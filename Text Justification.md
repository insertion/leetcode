 
 # question 
Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

For example,
words: ["This", "is", "an", "example", "of", "text", "justification."]
L: 16.

Return the formatted lines as:

[
   "This    is    an",
   "example  of text",
   "justification.  "
]
# solution
```c
class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) 
    {//引用形参，不拷贝实参，直接操作实参
        vector<string> res;
        int total=-1,i;
        int start=0,end;
        string temp="";
        int space_all,space,space_leave;
        for( i=0;i<words.size();i++)
        {
            total+=words[i].size()+1;//包括空格，因为最后字符后不加空格，所以total初始化为-1
            if(total>maxWidth)
            {
                end=i-1;
                space_all=maxWidth-total+words[i].size()+1;
                if(end==start)
                {
                temp+=words[start]+string(space_all,' ');
                }
                else
                {
                space=space_all/(end-start);//每个word后面该跟的空格数
                space_leave=space_all%(end-start);//剩余的空格数
                
                for(int j=start;j<end;j++)
                {
                  temp+=words[j]+string(space + 1 +(space_leave>j-start), ' '); 
                }
                temp+=words[end];
                }
                res.push_back(temp);
                temp="";
                start=i;//下一组的start从i开始
                i--;
                total=-1;
            }
            
        }
        end=i-1;
        space_all=maxWidth-total;
        if(end==start)
        {
        temp+=words[start]+string(space_all,' ');
        }
        else
        {
            
            for(int j=start;j<end;j++)
             {
              temp+=words[j]+string(1,' '); 
             }
             temp+=words[end]+string(space_all,' ');
        }
        
        res.push_back(temp);
        return res;
    }
};
```
# discussion
C语言在处理字符串的问题上比c++要弱很多，这题要考虑最后一行的特别情况，end==start的情况，每行的末尾的特殊情况