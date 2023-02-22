#include <ctype.h>
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// A node in the linked list

// Each string in the node is declared as a character pointer variable,
// so they need to be dynamically allocated using the malloc() function,
// and deallocated using the free() function after use.

// typedef struct node {
//   char *artist;
//   char *songName;
//   char *genre;
//   struct node *next;
// } Node;
typedef struct linkedlist{
  Node* head;
}LinkedList;
//

// Declarations of linked list functions
//
// DECLARE YOUR LINKED-LIST FUNCTIONS HERE
//

// Declarations of support functions
// See below the main function for descriptions of what these functions do

// void inputStringFromUser(char *prompt, char *s, int arraySize);
// void songNameDuplicate(char *songName);
// void songNameFound(char *songName);
// void songNameNotFound(char *songName);
// void songNameDeleted(char *songName);
// void artistFound(char *artist);
// void artistNotFound(char *artist);
// void printMusicLibraryEmpty(void);
// void printMusicLibraryTitle(void);

// const int MAX_LENGTH = 1024;
Node *createNode(char* song, char* artist, char* genre,int max) {
  Node *newNode = (Node *)malloc(sizeof(Node));
  newNode->songName=malloc((strlen(song)+1)*sizeof(char));
  newNode->artist=malloc((strlen(artist)+1)*sizeof(char));
  newNode->genre=malloc((strlen(genre)+1)*sizeof(char));

  if (newNode != NULL) {
    strncpy(newNode->songName,song,strlen(song));
    strncpy(newNode->artist,artist,strlen(artist));
    strncpy(newNode->genre,genre,strlen(genre));
    newNode->next = NULL;
  }
  return newNode;
  // free(newNode->songName);
  // free(newNode->artist);
  // free(newNode->genre);
}
bool isEmpty(LinkedList *list){
  if(list->head==NULL){
    return true;
  }
  return false;
}
void printList(LinkedList* list) {
  Node*current;
  current=list->head;
  if(current==NULL){
    return;
  }
  while (current!=NULL) {
    // Print out the data at this element.
    printf("\n%s\n", current->songName);
    printf("%s\n",current->artist);
    printf("%s\n",current->genre);
    // Move to the next element in the list.
    current = current->next;
  }
  
  
}
void initializeList(LinkedList* list) {
  // The head initially points to nothing.
  list->head=NULL;
}
void insertNode(LinkedList* list,char* song, char* artist, char* genre,int max){
  Node* current = createNode(song,artist,genre,max);
  Node* after = list->head;
  if(after==NULL||strcmp(song,after->songName)<0){
    if(current !=NULL){
      current->next=after;
      list->head = current;
      return;
    }
  }
  while(after->next!=NULL && strcmp(song,after->next->songName) > 0){
     after = after->next;
  }
  if(current!=NULL){
    current->next=after->next;
    after->next=current;
  }
}
bool duplicateName(LinkedList* list, char* song, char* artist, char* genre){
  Node* current;
  current=list->head;
  bool duplicate=false;
  bool done=false;
  if(current==NULL){
    duplicate=false;
    //printf("dddddddd");
  }
  while(current!=NULL&&!done){
    if(strcmp(song,current->songName)==0){
      duplicate=true;
      done=true;
      //printf("dddd");
    }
    current=current->next;
  }
  //printf("duplicate%d",duplicate);
  return duplicate;
}
bool songFind(LinkedList* list, char* song){
  Node* current;
  bool find=false;
  bool done = false;
  current=list->head;
  while(current!=NULL){
    if(strcmp(song,current->songName)==0&&!done){
      find=true;
      done=true;
    }
    current=current->next;
  }
  return find;
}
void deleteNode(LinkedList* list, char* song){
  Node* current;
  current=list->head;
  if (current==NULL){
    return;
  }
  if(strcmp(song,current->songName)==0){
    Node* newHead;
    newHead=current->next;
    free(current);
    list->head=newHead;
    return;
  }

  while(current->next!=NULL&&strcmp(song,current->next->songName)!=0){
    current=current->next;
  }
  if(current!=NULL){
    Node*temp=current->next;
    current->next=temp->next;
    free(temp);
  }
}
void deleteAllNode(LinkedList* list){
  Node* deleteAll;
  deleteAll=list->head;
  Node* remain;
  while(deleteAll!=NULL){
    songNameDeleted(deleteAll->songName);
    remain=deleteAll->next;
    free(deleteAll);
    deleteAll=remain;
  }
  printf("\nThe music library is empty.");
}
void printFindSongName(LinkedList* list,char*songName){
  //bool done = false;
  Node* address = list->head;
  while(address!=NULL){
    if(strcmp(songName,address->songName)==0){
      printf("\n%s\n",address->songName);
      printf("%s\n",address->artist);
      printf("%s\n",address->genre);
      return;
    }
    address=address->next;
  }
}
int main(void) {
  // Declare the head of the linked list.
  //   ADD YOUR STATEMENT(S) HERE
  LinkedList list;
  initializeList(&list);
  // Announce the start of the program
  printf("Personal Music Library.\n\n");
  printf("%s", "Commands are I (insert), D (delete), S (search by song name),\n"
               "P (print), Q (quit).\n");

  char response;
  char input[MAX_LENGTH + 1];
  char *songName = (char*)malloc(MAX_LENGTH*sizeof(char));
  char *artist = (char*)malloc(MAX_LENGTH*sizeof(char));
  char *genre = (char*)malloc(MAX_LENGTH*sizeof(char));
  do {
    inputStringFromUser("\nCommand", input, MAX_LENGTH);

    // Response is the first character entered by user.
    // Convert to uppercase to simplify later comparisons.
    //toupper is used to convert to upper case letter
    response = toupper(input[0]);
    //printf("********\n%c\n********\n", response);

    if (response == 'I') {
      
      // USE THE FOLLOWING STRINGS WHEN PROMPTING FOR DATA:
      char *promptName = "Song name" ;
      char *promptArtist =  "Artist" ;
      char *promptGenre = "Genre" ;
      inputStringFromUser(promptName,songName,MAX_LENGTH);
      inputStringFromUser(promptArtist,artist,MAX_LENGTH);
      inputStringFromUser(promptGenre,genre,MAX_LENGTH);
      if(!duplicateName(&list,songName,artist,genre)){
        insertNode(&list,songName,artist,genre,MAX_LENGTH);
        //printf("ddd");
      }else if(duplicateName(&list,songName,artist,genre)){
        songNameDuplicate(songName);
        //printf("重复了！");
      }
    

    } else if (response == 'D') {
      // Delete a song from the list.

      char *prompt = "\nEnter the name of the song to be deleted";

      //   ADD STATEMENT(S) HERE
      inputStringFromUser(prompt,songName,MAX_LENGTH);
      if(songFind(&list,songName)){
        deleteNode(&list,songName);
        songNameDeleted(songName);
      }else{
        songNameNotFound(songName);
      }

      
    } else if (response == 'S') {
      // Search for a song by its name.

      char *prompt = "\nEnter the name of the song to search for";

      //   ADD STATEMENT(S) HERE
      
      inputStringFromUser(prompt,songName,MAX_LENGTH);
      if(songFind(&list,songName)){
        songNameFound(songName);
        printFindSongName(&list,songName);
      }else if(!songFind(&list,songName)){
        songNameNotFound(songName);
      }
    } else if (response == 'P') {
      // Print the music library.

      //   ADD STATEMENT(S) HERE
      if(isEmpty(&list)){
        printMusicLibraryEmpty();
      }else if(!isEmpty(&list)){
        printMusicLibraryTitle();
        printList(&list);
      }
    } else if (response == 'Q') {
      // do nothing, we'll catch this below
    } else {
      // do this if no command matched ...
      printf("\nInvalid command.\n");
    }
  } while (response != 'Q');

  // Delete the entire linked list.
  //   ADD STATEMENT(S) HERE
  deleteAllNode(&list);
  // Print the linked list to confirm deletion.
  //   ADD STATEMENT(S) HERE

  return 0;
}
