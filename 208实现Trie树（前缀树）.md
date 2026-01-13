# ****https://leetcode.cn/problems/implement-trie-prefix-tree/
**🔗 题目链接：**  
**[implement-trie-prefix-tree](https://leetcode.cn/problems/implement-trie-prefix-tree/)**
---

## **解题代码（C++）**

```cpp
class Trie {
public:
Trie*next[26];
bool isEnd;
    Trie() {
        for(int i=0;i<26;i++)
        {
            this->next[i]=nullptr;
        }
        this->isEnd=false;
    }
    
    void insert(string word) {
        Trie*node=this;
        for(char c:word)
        {
            int num=c-'a';
            if(node->next[num]==nullptr)
            {
                node->next[num]=new Trie();
            }
            node=node->next[num];
        }
        node->isEnd=true;
    }
    
    bool search(string word) {
        Trie*node=this;
        for(char c:word)
        {
            int num=c-'a';
            if(node->next[num]==nullptr)
            return false;
            node=node->next[num];
        }
        return node->isEnd;
    }
    
    bool startsWith(string prefix) {
        Trie* node = this;
        for(char ch : prefix) {
            int idx = ch - 'a';
            if(node->next[idx] == nullptr)
                return false;  // 前缀不存在
            node = node->next[idx];
        }
        return true;            // 能走完整个前缀
    }
    
};

解题思路：
是最基础的字典树的建立，要记住它每层有多个节点，最多可达26个，因为总共有26个英文字母。
