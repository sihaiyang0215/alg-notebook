这题用的是拓扑排序
```java
class Solution {
    public String alienOrder(String[] words) {
        String ans = "";
        if(words == null || words.length == 0)
            return ans;
        //Build Graph
        Map<Character, Point> map = new HashMap<>();
        Trie trie = new Trie();
        for(String word : words)
            trie.insert(word, map);
        
        //Topological Sort
        Queue<Point> q = new LinkedList<>();
        for(Point p:map.values()){
            if(p.fathers.size() == 0)
                q.offer(p);
        }
    
        while(!q.isEmpty()){
            Point pt = q.poll();
            char c = pt.c;
            ans += c;
            for(char child : pt.children){
                Point p = map.get(child);
                if(p.fathers.size() > 0){
                    p.fathers.remove(c);
                    if(p.fathers.size() == 0)
                        q.offer(p);
                }
            }
        }
        if(ans.length() == map.size())
            return ans;
        return "";
    }
    
    class Point{
        char c;
        Set<Character> fathers;
        Set<Character> children;
        public Point(char c){
            this.c = c;
            fathers = new HashSet<>();
            children = new HashSet<>();
        }
    }
    
    class TrieNode{
        TrieNode[] children;
        char last;
        public TrieNode(){
            children = new TrieNode[26];
            last = ' ';
        }
        
        public void insert(String word, int index, Map<Character, Point> map){
            if(index == word.length())
                return;
            char cur = word.charAt(index);
            int pos = cur - 'a';
            
            //开始时候这里想错了。因为考虑到环的问题，如果children[pos]是null只需要建立一个新的TrieNode，
            //后面的一系列动作无论是否为null都需要做
            if(children[pos] == null)
                children[pos] = new TrieNode();
            
            Point tmp = map.getOrDefault(cur, new Point(cur));
            if(last != ' ' && last != cur){
                tmp.fathers.add(last);
                map.get(last).children.add(cur);
            }
            last = cur;
            map.put(cur, tmp);
            
            children[pos].insert(word, index + 1, map);
        }
    }
    
    class Trie{
        TrieNode root;
        public Trie(){
            root = new TrieNode();
        }
        public void insert(String word, Map<Character, Point> map) {
            root.insert(word, 0, map);
        }
    }
}
```
<b>建立Trie O(N * L) N是words长度L是每个word长度；建立Graph过程O(N * L)；Topological Sort: O(字母个数)。所以时间复杂度O(N * L); 空间复杂度O(N * L) + O(字母个数). 所以空间复杂度是O(N * L)。</b>
