#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct no {
	char dados;
	struct no* prox;
};
struct pilha {
	struct no* topo;
};
struct fila {
	struct no* frente;
	struct no* final;
};
//pilha dinamica
void push(struct pilha* s, char elemento) {
	struct no* novo_no = (struct no*)malloc(sizeof(struct no));
	novo_no->dados = elemento;
	novo_no->prox = s->	topo;
	s->topo = novo_no;
	
	
}
 char pop(struct pilha* s){
 	if(s->topo == NULL){
 		printf("pilha está vazia\n");
 		return '\0';
 		 }
 		 struct no* temp = s->topo;
 		 char popped = temp->dados;
 		 s->topo = temp->prox;
 		 free(temp);
 		 return popped;
 }
 // fila dinamica
  void enfileirar(struct fila* q, char elemento){
  	struct no* novo_no = (struct no*)malloc(sizeof(struct no));
  	novo_no->dados = elemento;
  	novo_no->prox = NULL;
  	if(q->final == NULL){
  		q->frente = novo_no;
  		q->final = novo_no;
  		return;	
	  }
	 q->final->prox = novo_no;
	 q->final = novo_no; 
  }
  char dfileirar(struct fila* q){
  	if(q->frente == NULL){
  		printf("Fila esta vazia\n");
  		return '\0';
  		
	  }
	  struct no* temp = q->frente;
	  char dfileirar  = temp->dados;
	  q->frente = temp->prox;
	  if(q->frente == NULL){
	  	q->final = NULL;
	  }
	  free(temp);
	  return dfileirar;
  	
  }
  void print_fila(struct fila* q){
  	if(q->frente == NULL){
  		printf("Fila está vazia\n");
  		return;
	  }
	  struct no* temp = q->frente;
	  while(temp != NULL) {
	  	printf("%c", temp->dados);
	  	temp = temp->prox;
	  	
	  }
	  printf("\n");
	  
	  
  }
  void print_pilha(struct pilha* s){
  	if(s->topo == NULL){
  		printf("A fila está vazia\n");
		  return;
	  }
	  struct no* temp = s->topo;
	  while(temp != NULL){
	  	printf("%c", temp->dados);
	  	temp = temp->prox;
	  }
	  printf("\n");
  }
  
  int main() {
  	char dna[100];
  	printf("DIGITE A SEQUENCIA DE DNA: ");
  	scanf("%s",dna);
  	struct fila q = {NULL, NULL};
  	struct pilha s = {NULL};
  	int n = strlen(dna);
  	for(int i = 0; i < n; i++){
  		enfileirar(&q, dna[i]);
  		
	  }
	  for(int i = 0; i < n; i++){
	  	char elemento = dfileirar(&q);
	  	if(elemento == 'A'){
	  		push(&s, 'T');
		  }else if(elemento == 'C'){
		  	push(&s, 'G');	
		  }else if(elemento == 'T'){
		  	push(&s, 'A');
		  }else if(elemento == 'G'){
		  	push(&s, 'C');
		  }
	  }
	printf("Fila:");
	print_fila(&q);
	printf("Pilha:");
	print_pilha(&s);
	return 0;
  	
  }
