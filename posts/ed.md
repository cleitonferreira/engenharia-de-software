# Estrutura de Dados e Algoritmos em C++

## Introdução
Estruturas de dados e algoritmos são essenciais na ciência da computação, pois são responsáveis pela organização, processamento e armazenamento eficiente de dados. Este artigo vai cobrir os conceitos mais importantes de forma simples e prática, usando a linguagem C++.

## Estruturas de Dados

### 1. Arrays
Arrays são coleções de elementos de mesmo tipo, armazenados em posições contíguas de memória.

#### Exemplo em C++:

Vamos criar uma lista sequencial para armazenar contatos

```cpp
#include <iostream>
#include <string>
#include <optional>


using namespace std;


class Contact
{
public:
    string name;
    string phone;
    string toString(){
        return "Name: " + name + " Phone: " + phone;
    }


};


class SequentialList
{
private:
    Contact *array; // Ponteiro para armazenar os elements da list
    int length;     // Tamanho atual da list


public:
    // Construtor da classe SequentialList+
    SequentialList()
    {
        length = 0;         // Inicializa o length da list como 0
        array = new Contact[0]; // Inicializa o ponteiro para o array vazio
    }


    // Destrutor da classe SequentialList
    ~SequentialList()
    {
        delete[] array; // Libera a memória alocada para o array
    }


    // Verifica se a list está vazia
    bool isEmpty()
    {
        return length == 0; // Retorna verdadeiro se o length da list for igual a 0
    }


    // Insere um element na list
    void add(Contact element)
    {
        Contact *newArray = new Contact[length + 1]; // Aloca um novo array com espaço para o novo element
        for (int i = 0; i < length; i++)
        {
            newArray[i] = array[i]; // Copia os elements do array original para o novo array
        }
        newArray[length++] = element; // Insere um element no novo array e em seguida tamanho aumenta um
        delete[] array;               // Libera a memória alocada para o array original
        array = newArray;             // Atualiza o ponteiro para apontar para o novo array
    }


    // retorna um element do array
    std::optional<Contact> get(int index)
    {
        if (!isEmpty() && !(index < 0 || index > length - 1))
        {
            return array[index];
        }else{
            return std::nullopt;
        }
    }
    bool remove(int index)
    {
        if (index < 0 || index > length - 1)
        {
            return false;
        }
        for (int i = index; i < length - 1; i++)//move todos os elementos para a esquerda
        {
            array[i] = array[i + 1];
        }
        length--;   //diminue o tamanho
        return true;//retorna true
    }
    int getLength()
    {
        return length;
    }
};


int main()
{
    SequentialList list;


    while (true)
    {
        cout << "Selecione um comando:\n";
        cout << "1 - Adicionar\n";
        cout << "2 - remover\n";
        cout << "3 - listar\n";


        int command;
        cin >> command;






        if (command == 0)
        {
            break;
        }
        else if (command == 1)
        {
            Contact contact;
            cout << "Digite o nome:";
            cin >> contact.name;
            cout << "Digite o telefone";
            cin >> contact.phone;
            list.add(contact);
        }
        else if (command == 2)
        {
            int index;
            cin >> index;
            list.remove(index);
        }
        else if (command == 3)
        {
              for (int i = 0; i < list.getLength(); i++) {
                auto contact = list.get(i);
                if (contact.has_value()) {
                    cout << contact.value().toString() << "\n";
                } else {
                    cout << "Elemento inválido.\n";
                }
            }
        }
        else
        {
            cout << "comando invalido!\n";
        }
    }


    return 0;
}




```