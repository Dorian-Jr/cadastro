
using namespace std;

struct Usuario {
	string nome;
	int idade;
	string email;
};

void adicionarUsuario() {
	Usuario usuario;
	
	cout << "Digite o nome do usuário: ";
	cin.ignore();
	getline(cin, usuario.nome);
	
	cout << "Digite a idade do usuário: ";
	cin >> usuario.idade;
	
	cout << "Digite o email do usuário: ";
	cin.ignore();
	getline(cin, usuario.email);
	
	ofstream arquivo("usuario.txt", ios::app);
	
	if (arquivo.is_open()) {
		arquivo << usuario.nome << "," << usuario.idade << "," << usuario.email << endl;
		arquivo.close();
		
		cout << "Usuario adicionado com sucesso." << endl;
	} else {
		cout << " Erro ao abrir o arquivo." << endl;
	}
}

 void visualizarUsuario() {
 	ifstream arquivo("usuario.txt");
 	
 	if (arquivo.is_open()) {
 		string linha;
 		
 		while (getline(arquivo, linha)) {
 			cout << linha << endl;
		 }
		 
		 arquivo.close();
	} else {
		cout << "Erro ao abrir o arquivo." << endl;
	 }
 }
 
 void editarUsuario() {
 	string nomeAntigo;
 	cout << "Digite o nome do usuário que deseja editar: ";
 	cin.ignore();
 	getline(cin, nomeAntigo);
 	
 	ifstream arquivoAntigo("usuario.txt");
 	
 	if (arquivoAntigo.is_open()) {
 		string linha;
 		string conteudoNovo;
 		string arquivoTemporario = "temp.txt";
 		
 		ofstream arquivoNovo(arquivoTemporario.c_str());
 		
 		if (arquivoNovo.is_open()) {
 			while (getline(arquivoAntigo, linha)) {
 				size_t posicao = linha.find(nomeAntigo);
 				if (posicao != string::npos) {
 					cout << "Digite o novo nome do usuário: ";
 					getline( cin, conteudoNovo);
 					linha.replace(posicao, nomeAntigo.length(), conteudoNovo);
				 }
				 arquivoNovo << linha << endl;
			 }
			 
			 arquivoAntigo.close();
			 arquivoNovo.close();
			 
			 remove("usuarios.txt");
			 rename("temp.txt", "usuarios.txt");
			 
			 cout << "Usuário editado com sucesso." << endl;
		 } else {
		 	 cout << "Erro ao abrir o arquivo temporario." << endl;
		 }
	} else {
		cout << "Erro ao abrir o arquivo antigo." << endl;
	 }
 }
 
 void excluirUsuario() {
 	string nomeUsuario;
 	cout << "Digite o nome do usuário que deseja excluir: ";
 	cin.ignore();
 	getline(cin, nomeUsuario);
 	
 	ifstream arquivoAntigo("usuario.txt");
 	
 	if (arquivoAntigo.is_open()) {
 		string linha;
 		string arquivoTemporario = "temp.txt";
 		
 		ofstream arquivoNovo(arquivoTemporario.c_str());
 		
 		if (arquivoNovo.is_open()) {
 			while (getline(arquivoAntigo, linha)) {
 				size_t posicao = linha.find(nomeUsuario);
 				if (posicao == string::npos) {
 					arquivoNovo << linha << endl;
				 }
			 }
 			
 			arquivoAntigo.close();
 			arquivoNovo.close();
 			
 			remove("usuarios.txt");
 			rename("temp.txt", "usuarios.txt");
 			
 			cout << "Usuário excluido com sucesso." << endl;
 		} else {
 			cout << "Erro ao abrir o arquivo temporário." << endl;
 		}
 	} else {
 		cout << "Erro ao abrir o arquivo antigo." << endl;
	 }
 }
 
 int main() {
 	int opcao;
 	
 	cout << "Bem-vindo ao sistema de Cadastro!" << endl;
 	
 	do {
 		cout << "Selecione uma opção:" << endl;
 		cout << "1 - Adicionar usuário" << endl;
 		cout << "2 - Visualizar usuarios" << endl;
 		cout << "3 - Editar usuário" << endl;
 		cout << "4 - Excluir usuário" << endl;
 		cout << "5 - Sair" << endl;
 		cin >> opcao;
 		
 		switch (opcao) {
 			case 1:
 				adicionarUsuario();
 				break;
 			case 2:
 				visualizarUsuario();
 				break;
 			case 3:
 				editarUsuario();
 				break;
 			case 4:
 				excluirUsuario();
 				break;
 			case 5:
 				cout << "Encerrando o programa..." << endl;
 				break;
 			default:
 				cout << "Opção invalida." << endl;
 				break;
		 }
	 } while (opcao != 5);
	 
	 return 0;
 }
