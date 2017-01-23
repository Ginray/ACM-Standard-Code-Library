````
include <iostream>

include <string>

include <cstring>

using namespace std;

void findBMstr(string& str)

{

    int *p = new int[str.size() + 1];
    memset(p, 0, sizeof(p));
    
    int mx = 0, id = 0;
    for(int i = 1; i <=  str.size(); i++)
    {
        if(mx > i)
        {
            p[i] = (p[2*id - i] < (mx - i) ? p[2*id - i] : (mx - i));
        }
        else
        {
            p[i] = 1;
        }
    
        while(str[i - p[i]] == str[i + p[i]])
            p[i]++;
    
        if(i + p[i] > mx)
        {
            mx = i + p[i];
            id = i;
        }
    
    }
    int max = 0, ii;
    for(int i = 1; i < str.size(); i++)
    {
        if(p[i] > max)
        {
            ii = i;
            max = p[i];
        }
    }
    
    max--;
    
    int start = ii - max ;
    int end = ii + max;
    for(int i = start; i <= end; i++)
    {
        if(str[i] != '#')
        {
            cout << str[i];
        }
    }
    cout << endl;
    
    delete  p;

}

int main()

{

    string str = "12212321";
    string str0;
    str0 += "$#";
    for(int i = 0; i < str.size(); i++)
    {
        str0 += str[i];
        str0 += "#";
    }
    
    cout << str0 << endl;
    findBMstr(str0);
    return 0;

}

````




