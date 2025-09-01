//Equipe: Bianca Lima, Júlia Ribeiro e Larissa Rocha
//Tema: Ganhadores de Oscar

#include <iostream>
#include <fstream>
#include <cstring>
#include <stdio.h>

using namespace std;

struct ganhadores{
  char nome[23];
  char modalidade [30];
  char filme [40];
  int ano;
  char pais[16];
  int duracaoMin;
};



//Procedimento para trocar dois elementos de tipo ganhadores

void trocar(ganhadores &a, ganhadores &b){
    ganhadores temp = a;
    a = b;
    b = temp;
}

//Função para fazer particionamento por ano de premiação

int particionarAno(ganhadores lista[], int inicio, int fim) {
    int pivo = lista[fim].ano;
    int i = inicio - 1;

    for (int j = inicio; j < fim; j++) {
        if (lista[j].ano <= pivo) {
            i++;
            swap(lista[i], lista[j]);
        }
    }
    swap(lista[i + 1], lista[fim]);

    return i + 1;
}

//Função para fazer o particionamento por nome do ganhador

int particionarNome(ganhadores lista[], int inicio, int fim) {
    char pivo[23];
    strcpy(pivo, lista[fim].nome);
    int i = inicio - 1;

    for (int j = inicio; j < fim; j++) {
        if (strcmp(lista[j].nome, pivo) <= 0) {
            i++;
            swap(lista[i], lista[j]);
        }
    }
    swap(lista[i + 1], lista[fim]);

    return i + 1;
}

//Procedimento Quick Sort para ordenar por ano de premiação

void quickSortAno(ganhadores lista[], int inicio, int fim) {
    if (inicio < fim) {
        int pivo = particionarAno(lista, inicio, fim);

        quickSortAno(lista, inicio, pivo - 1);
        quickSortAno(lista, pivo + 1, fim);
    }
}

// Procedimento Quick Sort para ordenar por nome do ganhador

void quickSortNome(ganhadores lista[], int inicio, int fim) {
    if (inicio < fim) {
        int pivo = particionarNome(lista, inicio, fim);

        quickSortNome(lista, inicio, pivo - 1);
        quickSortNome(lista, pivo + 1, fim);
    }
}

//Remoção para sobreescrever se dá por negativação da duração do filme.
//Remoção definitiva será feita ao reorganizar o arquivo.
void remover(ganhadores lista[], int tam, int remove){
  for (int i=0; i<tam; i++){
    if (i==remove){
      lista[i].duracaoMin = -1;
    }
  }
}

//Escreve no arquivo "oscar.dat" 

void GravarBinario(ganhadores lista[], int i){
  ofstream novoArqbin ("oscar.dat", ios::binary);
  novoArqbin.write((char*)lista, sizeof(ganhadores)*i);
}

//Escreve no arquivo "novo_oscar.csv" 

void CSV(ganhadores lista[], int i){
  ofstream arquivoCSV ("novo_oscar.csv");
  for (int j=0; j<i; j++){
  arquivoCSV<<lista[j].nome<<","<<lista[j].modalidade<<","<<lista[j].filme<<","<<lista[j].ano<<","<<lista[j].pais<<","<<lista[j].duracaoMin<<endl;  
  }

}


//Pede entrada do usuário para inserir novos dados no arquivo

void dadosNovos(ganhadores lista[], int i ){
    cin.ignore();
    cout<<"Digite o nome do ganhador: ";
        cin.getline(lista[i].nome,23);
        cout<<"Digite a modalidade do ganhador: ";
        cin.getline(lista[i].modalidade,30);
        cout<<"Digite o nome do filme: ";
        cin.getline(lista[i].filme,40);
        cout<<"Digite o ano de produção: ";
        cin>>lista[i].ano;
        cin.ignore();
        cout<< "Digite o país de origem do filme: ";
        cin.getline(lista[i].pais,16);
        cout<<"Digite a duração do filme em minutos: ";
        cin>>lista[i].duracaoMin;
}


bool buscarAno( ganhadores lista[], int i , int buscaAno){	
  if (buscaAno==lista[i].ano){
    cout <<i+1<<" "<<lista[i].nome<< " "<<lista[i].modalidade<<" "<< lista[i].filme<<" "<<lista[i].ano<<" "<<lista[i].pais<<" "<<lista[i].duracaoMin<< endl;
    return true;
  }else {
  return false;  
  }
}

void imprimir(ganhadores lista[], int i)
{
  cout << lista[i].nome<< " "<<lista[i].modalidade<<" "<< lista[i].filme<<" "<<lista[i].ano<<" "<<lista[i].pais<<" "<<lista[i].duracaoMin<<endl;

}

int main(){

  int escolha;
  int busca;
  int buscaAno;
  string buscaGanhador;
  int tam=0;
  int imp;
  int insere;
  int remove;
  int ordena;

//Importação do CSV para arquivo binário
    ifstream arqCSV ("oscar.csv");
  char lixo;
  ganhadores listacsv [50];
  for (int i=0; i<50; i++){
    arqCSV.getline(listacsv[i].nome, 23, ',');
    arqCSV.getline(listacsv[i].modalidade, 30, ',');
    arqCSV.getline(listacsv[i].filme,40,',');
    arqCSV>>listacsv[i].ano;
    arqCSV>>lixo;
    arqCSV.getline(listacsv[i].pais, 16, ',');
    arqCSV>>listacsv[i].duracaoMin;
    arqCSV.ignore();
  }




    ofstream arqbin ("oscar.dat", ios::binary);
    arqbin.write((char*)listacsv, sizeof(ganhadores)*50);


//Redimensionamento de vetor de registros para leitura completa do arquivo binário e acréscimo na variável tam para cada registro lido do arquivo 
  ifstream arquivobinario("oscar.dat", ios::binary);
  ganhadores* lista = nullptr;
  ganhadores registro;

  while (arquivobinario.read(reinterpret_cast<char*>(&registro), sizeof(ganhadores))) {
      tam++;
      ganhadores* temp = new ganhadores[tam];
      if (lista) {
          memcpy(temp, lista, (tam - 1) * sizeof(ganhadores));
          delete[] lista;
      }
      lista = temp;
      lista[tam - 1] = registro;
  }



//Primeira entrada

  while(true){
  cout << "Digite 1 para remover dados existentes" << endl << "Digite 2 para gravar um novo elemento no arquivo" <<endl<< "Digite 3 para buscar registro" << endl << "Digite 4 para imprimir arquivo" << endl<< "Digite 5 para exportar arquivo para CSV"<<endl<<"Digite 6 para ordenar o arquivo"<<endl;
  cin >> escolha;

//Pede entrada do usuário e marca com chave negativa lista[entrada].duracaoMin

    if(escolha==1){
    cout << "Digite o índice do vetor que deseja apagar:";
    cin>>remove;
    remover(lista, tam, remove);
    GravarBinario(lista, tam);
    cout<<"Índice marcado com chave negativa!"<<endl;
    }

    else if(escolha==2){
    cout << "Caso tenha algum elemento marcado com chave negativa (removido) a inserção ocorrerá sobreescrevendo esse dado."<<endl<<"Caso contrário a inserção ocorrerá no fim do arquivo."<<endl;
    bool reescrever = false;

  //Sobreescreve elemento marcado com chave negativa caso esse exista

    for (int i=0; i<tam; i++){
      if (lista[i].duracaoMin==-1){
      reescrever=true;
      dadosNovos(lista, i);
      GravarBinario (lista, tam);
      }
    }

  //Insere elemento novo no fim do arquivo

    if (reescrever==false){
      insere=1;
      ganhadores *temp = new ganhadores [tam+insere];
      memcpy(temp, lista, sizeof(ganhadores)*tam);
      delete [] lista;
      lista = temp;

      for (int i=tam; i<(tam+insere); i++){
      dadosNovos(lista, i);
      }
    tam= tam+insere;
    GravarBinario(lista, tam);
    }

     cout<<"Elemento inserido com sucesso!"<<endl;
    }

  //Busca em regitro de dois tipos diferentes (comparação de char e de inteiros)

    else if(escolha==3){
    cout << "Digite 1 para fazer busca por ano de premiação"<<endl<<"Digite 2 para fazer busca por nome do ganhador"<<endl;
    cin>>busca;
    if (busca==1){
      cout<<"Digite o ano de premiação: ";
      cin>>buscaAno;
      int i=0;
      while (i<tam and (buscarAno(lista, i, buscaAno)==false) ){
      i++;
      }
      if (buscarAno(lista, i, buscaAno)==false){
      cout<<"Ano de premiação não encontrado."<<endl;
      }
    }else if (busca==2){
      cout<< "Digite o nome do ganhador: ";
      cin.ignore();
      getline (cin, buscaGanhador);
      bool achou=false;
      int i=0;
      while (i<tam and achou==false){
      if (strcmp(buscaGanhador.c_str(),lista[i].nome)==0){
        achou=true;
        cout <<i+1<<" "<< lista[i].nome<< " "        
        <<lista[i].modalidade<<" "<<         
        lista[i].filme<<" "<<lista[i].ano<<" "  
        <<lista[i].pais<<" "<<lista[i].duracaoMin<<   
        endl;
      }
       i++;
     }
     if (achou==false){
      cout<<"Nome do ganhador não encontrado."<<endl;
     }
    }
    }

  //Imprime arquivo completo ou trecho, dependendo da entrada do usuário

    else if(escolha==4){
    cout<<"Digite 1 para imprimir arquivo completo"<<endl<<"Digite 2 para imprimir trecho de vetor"<<endl;
    cin>>imp;
    if (imp==1){
      for (int i=0; i<tam; i++){
      imprimir(lista, i);
      }
    }
    else{
      int inicio, fim;
      cout<< "Digite o inicio do vetor"<<endl;
      cin>>inicio;
      cout<<"Digite o fim do vetor"<<endl;
      cin>>fim;
      for (int i=inicio; i<=fim; i++){
      imprimir(lista, i);
      }
    }
    }

  //Chama procedimento de exportação para CSV

    else if (escolha==5){
    CSV (lista,tam); 
    cout << "Exportação concluída com sucesso!" << endl; 
    }

  //Ordenação por dois campos diferentes

    else if (escolha==6){
      //Remoção definitiva de elementos marcados com chave negativa
      int j=0;
      ganhadores lista2 [tam];
      for (int i=0; i<tam; i++){
        if (lista[i].duracaoMin!=-1){
          lista2[j]=lista[i];
         j++;
        }
      }
      for (int i = 0; i < j; i++) {
        lista[i]=lista2[i];
      }
      tam=j;
      GravarBinario (lista,tam);

     cout<<"Digite 1 para ordenar crescentemente o arquivo por ano de premiação"<<endl<<"Digite 2 para ordenar crescentemente o arquivo por nome do ator premiado"<<endl;
      cin>>ordena;
      if(ordena==1){
        quickSortAno(lista, 0, tam-1);
        GravarBinario(lista, tam);
      }else if (ordena==2){
        quickSortNome(lista, 0, tam-1);
        GravarBinario(lista, tam);
      }
      cout<<"Ordenação concluída com sucesso!"<<endl;
    }


  //Retorna função main() caso a entrada seja inválida

    else{
    cout << "Opção não encontrada." << endl;
    cout << main() << endl;
    }
}

  return 0;
}
