#include<iostream>
#include<string.h>
#include<stdlib.h>
#include<stdio.h>

using namespace std;

class frame_the_phrase
{
public:
    int option;
    char phrase[100], framechar;
    char line[30];
    char words[50][20], lines[50][30];

    friend istream &operator>>( istream  &input, frame_the_phrase &ph )
    {
        input>>ph.option;
        return input;
    }

    friend ostream &operator<<( ostream &output, const frame_the_phrase &ph )
    {
        output<<ph.line;
        return output;
    }

    void divide_words();
    void create_frame(int side);
};

int cnt;

void frame_the_phrase::divide_words()
{
    int phraselen = strlen(phrase);
    cnt=0;
    int i, j=0;
    for(i=0;i<phraselen;i++)
    {
        if(phrase[i]==' ')
        {
            words[cnt][j]='\0';
            cnt++;
            j=0;
        }
        else
        {
            words[cnt][j] = phrase[i];
            j++;
        }
    }
    words[cnt][j]='\0';
    cnt++;
}

void frame_the_phrase::create_frame(int side)
{
    int i, j, k, longest=0, currlen, emptylen, pre, post;
    for(i=0;i<cnt;i++)
    {
        if(strlen(words[i]) > longest)
            longest=strlen(words[i]);
    }

    for(j=0;j<longest+4;j++)
        lines[0][j]=framechar;
    lines[0][j]='\0';

    for(i=0;i<cnt;i++)
    {
        currlen=strlen(words[i]);
        emptylen=longest-currlen;
        switch(side)
        {
            default:
                cout<<"\nWrong choice! Center chosen as default";
            case 1:
                pre=(emptylen/2) + 1;
                post=(emptylen-pre) + 2;
                break;
            case 2:
                pre=1;
                post=emptylen + 1;
                break;
            case 3:
                pre=emptylen + 1;
                post=1;
                break;
        }
        lines[i+1][0]=framechar;
        for(j=0;j<pre;j++)
            lines[i+1][j+1]=' ';
        j++;
        for(k=0;k<currlen;k++)
            lines[i+1][j++] = words[i][k];
        for(k=0;k<post;k++)
            lines[i+1][j++]=' ';
        lines[i+1][j]=framechar;
        j++;
        lines[i+1][j]='\0';
    }
    i++;
    for(j=0;j<longest+4;j++)
        lines[i][j]=framechar;
    lines[i][j]='\0';
}

int main()
{
    frame_the_phrase ph;
    char fname[20];
    int choice, i, j;
    cout<<"\nRead Phrase from: ";
    cout<<"\n1. Keyboard";
    cout<<"\n2. File";
    cout<<"\nEnter your Option: ";
    cin>>ph;
    switch (ph.option)
    {
        case 1:
            cout<<"\n\nEnter Phrase: ";
            std::cin.getline(ph.phrase,100);
            std::cin.getline(ph.phrase,100);
            break;
        case 2:
            cout<<"\n\nEnter File name: ";
            cin>>fname;
            FILE *text;
            text = fopen(fname, "r");  /*  open the file for reading  */
            if (!text)
            {
                cout<<"\nError opening File!";
                exit(1);
            }
            int c;
            i=0;
            while ((c = getc(text)) != EOF)
            {
                ph.phrase[i] = c;
                i++;
            }
            ph.phrase[i] = '\0';
            fclose(text);
            break;
        default:
            cout<<"\nWrong Choice!";
            exit(0);
    }
    char ch;
    cout<<"\n\nWhat character you are to make the frame from ( for example '#'? )  ";
    cout<<"\nEnter your Choice: ";
    cin>>ch;
    if( !isprint(ch) )
    {
        cout<<"\nCharacter can't be printed!";
        exit(0);
    }
    ph.framechar=ch;
    int side;
    cout<<"\n\nFraming justification side.. ";
    cout<<"\n1. Center";
    cout<<"\n2. Left";
    cout<<"\n3. Right";
    cout<<"\nEnter your Choice: ";
    cin>>side;
    ph.divide_words();
    ph.create_frame(side);
    cout<<"\nChoose if the framed phrase is to be: ";
    cout<<"\n1. Printed on the screen ";
    cout<<"\n2. Saved into a file";
    cout<<"\nEnter your choice: ";
    cin>>ph;
    switch (ph.option)
    {
        case 1:
            cout<<"\n";
            for(i=0;i<cnt+2;i++)
            {
                strcpy(ph.line, ph.lines[i]);
                cout<<ph<<endl;
            }
            break;
        case 2:
            cout<<"\n\nEnter file name(Append Mode): ";
            cin>>fname;
            FILE *text;
            text = fopen(fname, "a+");  /*  open the file for writing in append mode  */
            if (!text)
            {
                cout<<"\nError opening File!";
                exit(1);
            }
            int c;
            i=0;
            for(i=0;i<cnt+2;i++)
            {
                for(j=0;ph.lines[i][j]!='\0';j++)
                {
                    c = ph.lines[i][j];
                    putc(c, text);
                }
                c = '\n';
                putc(c, text);
            }
            cout<<"\nOutput saved in file successfully.\n";
            fclose(text);
            break;
        default:
            cout<<"\nWrong Choice!";
    }
    return 0;
}
