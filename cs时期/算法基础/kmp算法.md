什么是kmp算法？
字符串匹配：顺序匹配，用已有信息指导单字符不匹配后的情况处理。
	  `while (j > 0 && p[i - 1] != p[j]) j = ne[j];`


应用一：某字符串所有前缀串的最长相同前后缀
```cpp
vector<int> build_next_1based(const string& p) {
    int m = (int)p.size();
    vector<int> ne(m + 1, 0); // ne[1..m]
    for (int i = 2, j = 0; i <= m; i++) {
        while (j > 0 && p[i - 1] != p[j]) j = ne[j];
        if (p[i - 1] == p[j]) j++;
        ne[i] = j;
    }
    return ne;
}
```

应用二：字符串b在字符串a中的所有出现位置

```cpp
vector<int> find_pos(const string& s1, const string& s2) {
	vector<int> ans;
	vector<int> next = build_next_1based(s2);
	int k=0;
    for (int i=0;i<s1.length();i++){
        while (k > 0 && s1[i] != s2[k]) k = next[k];
        if (s1[i] == s2[k]) k++;
        if (k == s2.length()) {
            ans.push_back(i+2-s2.length());
            k = next[k];
        }
    }
    return ans;
}
```