    #include <iostream>
    #include <cstring>
    using namespace std;
    
    int strStr(char *haystack, char *needle)
    {
        int len1 = strlen(haystack);
    	int len2 = strlen(needle);
    
    	int charStep[256];
    	for (int i = 0; i < 256; ++i)
    		charStep[i] = -1;
    	for (int i = 0; i < len2; ++i)
    		charStep[(int)needle[i]] = i;
    
    	for (int i = 0; i <= len1 - len2;)
    	{
    		int j = 0;
    		while (j < len2) {
    			if (haystack[i] == needle[j]) {
    				++i;
    				++j;
    			} else {
    				char* p = haystack + i + len2 - j;
    				if (charStep[(int)*p] == -1) {
    					i = p - haystack + 1;
    				} else {
    					i = p - charStep[(int)*p] - haystack;
    				}
    				break;
    			}
    		}
    
    		if (j == len2) {
    			return i - len2;
    		}
    	}
    
    	return -1;
    }
    
    int main()
    {
        char src[]="abcdezzz";
        char des[]="abcdezzz";
        cout<<strStr(src,des)<<endl;  //-1是匹配不成功  0是匹配成功
        return 0;
    }
