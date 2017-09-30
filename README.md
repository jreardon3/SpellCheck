# SpellCheck
File I/O Program that reads in file and returns misspelled words in new file (can be modified to cout output -- check comments)
//  main.cpp
//  SpellChecker
//
//  Created by Jacqueline Reardon on 9/29/17.
//  Copyright © 2017 Jacqueline Reardon. All rights reserved.
//

#include <iostream>
#include <fstream>
#include <cstdlib>
#include <unordered_set>
#include <string>
#include <vector>
using namespace std;

int main() {
    ifstream words_in;
    ifstream input_dict;
    ofstream output_misspelled_words;
    words_in.open("/Users/jreardon/Library/Mobile Documents/com~apple~TextEdit/Documents/words_spellcheck.txt");
    input_dict.open("/Users/jreardon/Library/Mobile Documents/com~apple~TextEdit/Documents/dictionary_ad_spellcheck.txt");
    output_misspelled_words.open("/Users/jreardon/Library/Mobile Documents/com~apple~TextEdit/Documents/output_spellcheck.txt");
    if (words_in.fail() || input_dict.fail()){
        cout<< "Input file opening failed."<<endl;
        exit(1);
    }
    string d, words;
    vector<string> misspelled_words;
    unordered_set<string> dictionary;
    while (input_dict>>d){
        dictionary.insert(d);
    }
    if (output_misspelled_words.fail()){
        cout<< "Output file opening failed."<<endl;
        exit(1);
    }
    while(words_in>>words){
        if(dictionary.find(words)==dictionary.end()){
            misspelled_words.push_back(words);
            if(words==misspelled_words[0] && words!=misspelled_words[misspelled_words.size()]){
                output_misspelled_words<<"Your misspelled words are: "<<endl;
                output_misspelled_words<<words<<", ";
                //cout<<"Your misspelled words are: "<<endl;
                //cout<<words<<", ";
            }
            else{
                output_misspelled_words<<words<<endl;
                //cout<<words<<endl;
            }
        }
    }
    if (misspelled_words.size()==0){
        output_misspelled_words<<"No misspellings. Good job!"<<endl;
        //cout<<"No misspellings. Good job!"<<endl;
    }
    words_in.close();
    input_dict.close();
    output_misspelled_words.close();
}
