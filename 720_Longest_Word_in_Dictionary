# Problem

Given a list of strings words representing an English Dictionary, find the longest word in words that can be built one character at a time by other words in words. If there is more than one possible answer, return the longest word with the smallest lexicographical order.

If there is no answer, return the empty string.
Example 1:
Input: 
words = ["w","wo","wor","worl", "world"]
Output: "world"
Explanation: 
The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
Example 2:
Input: 
words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]
Output: "apple"
Explanation: 
Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".
Note:

All the strings in the input will only contain lowercase letters.
The length of words will be in the range [1, 1000].
The length of words[i] will be in the range [1, 30].

# Solution 1
1. build a word tree
2. search the longest word from the tree

```
class Solution {
    private TreeNode wordTree = new TreeNode();
    
    public String longestWord(String[] words) {
        for(String word : words) {
            buildTree(word);
        }
        
        return getWord(wordTree);
    }
    
    private void buildTree(String word) {
        if(wordTree.getChildren().isEmpty())
            wordTree.addChild(new TreeNode(word));
        else {
            boolean found = false;
            for(TreeNode child : wordTree.getChildren()) {
                System.out.println(child.getWord() + "-------" + word);
                if(child.getWord().startsWith(word) 
                   || word.startsWith(child.getWord())) {
                    insertNote(child, word);
                    found = true;
                    break;
                }
                    
            }
            if(!found)
                wordTree.addChild(new TreeNode(word));
        }    
       
    }
    
    private void insertNote(TreeNode treeNode, String word) {
        TreeNode newNode = new TreeNode(word);
        if(treeNode.getWord().startsWith(word))
        {
            if(treeNode.getParent() == null) {
                treeNode.setParent(newNode);
                return;
            }
            else {
                insertNote(treeNode.getParent(), word);
            }
        }
        else if (treeNode.getChildren().isEmpty()) {
            treeNode.addChild(newNode);
        }
        else {
            // word starts with treeNode.getword
            List<TreeNode> newChildren = new ArrayList<>();
            for(TreeNode child : treeNode.getChildren()) {
                if(child.getWord().startsWith(word)) {
                    child.setParent(newNode);
                    newChildren.add(child);
                }
                    
            }
            
            newNode.getChildren().addAll(newChildren);
            treeNode.getChildren().removeAll(newChildren);
            treeNode.getChildren().add(newNode);
            newNode.setParent(treeNode);
        }
    }
    
    private String getWord(TreeNode treeNode) {
        System.out.println(treeNode.getWord());
        System.out.println(treeNode.getChildren().size());
        if(treeNode.getChildren().isEmpty() 
           && treeNode.getParent() != null 
           && treeNode.getParent().getWord() != null)
            return treeNode.getWord();
        
        String longestWord = "";
        String word = "";
        for(TreeNode child : treeNode.getChildren()) {
            word = getWord(child);
            if(word.length() > longestWord.length())
                longestWord = word;
            else if (word.length() == longestWord.length()
                    && word.compareTo(longestWord) < 0)
                longestWord = word;
        }
        return longestWord;
    }
}

public class TreeNode {
    private String word;
    private TreeNode parent ;
    private List<TreeNode> children= new ArrayList<>();
    
    public TreeNode(){}
    
    public TreeNode(String word) {
        this.word = word;
    }
    
    public void addChild(TreeNode child) {
        children.add(child);
    }
    
    public List<TreeNode> getChildren() {
        return children;
    }
    
    public void setParent(TreeNode parent) {
        this.parent = parent;
    }
    
    public TreeNode getParent() {
        return parent;
    }
    
    public String getWord() {
        return word;
    }
}


```

# Solution 1 bug fix
Now solution passed the test, but the performance is really poor!!!
1. Use a set to store data avoid duplicate words
2. fixed build tree logic 
3. added depth when searching a longest word. Only return word when depth match the word length

```
class Solution {
    private TreeNode wordTree = new TreeNode();
    
    public String longestWord(String[] words) {
        // avoid duplicate words
        Set<String> wordSet = new HashSet<>();
        wordSet.addAll(Arrays.asList(words));
        for(String word : wordSet) {
            buildTree(word);
        }
        
        return getWord(wordTree, 0);
    }
    
    private void buildTree(String word) {
        TreeNode newNode = new TreeNode(word);
        newNode.setParent(wordTree);
        
        if(wordTree.getChildren().isEmpty()) {
            wordTree.addChild(newNode);
        }
        else {
            boolean found = false;
            for(TreeNode child : wordTree.getChildren()) {
                System.out.println(child.getWord() + "-------" + word);
                if(child.getWord().equals(word))
                    return;
                else if(child.getWord().startsWith(word) 
                   || word.startsWith(child.getWord())) {
                    insertNote(child, word);
                    found = true;
                    break;
                }
                    
            }
            if(!found) {
                wordTree.addChild(newNode);
            }
                
        }    
       
    }
    
    private void insertNote(TreeNode treeNode, String word) {
        TreeNode newNode = new TreeNode(word);
        if(treeNode.getWord() != null && treeNode.getWord().startsWith(word))
        {
            if(treeNode.getParent() == null) {
                treeNode.setParent(newNode);
                System.out.println("setting parent " + newNode.getWord() + " to " + treeNode.getWord());
                return;
            }
            else {
                insertNote(treeNode.getParent(), word);
            }
        }
        else if (treeNode.getChildren().isEmpty()) {
             System.out.println("setting child " + newNode.getWord() + " to " + treeNode.getWord());
            treeNode.addChild(newNode);
        }
        else {
            // word starts with treeNode.getword
            List<TreeNode> newChildren = new ArrayList<>();
            for(TreeNode child : treeNode.getChildren()) {
                if(child.getWord().startsWith(word)) {
                    child.setParent(newNode);
                    newChildren.add(child);
                }
                else if(word.startsWith(child.getWord())) {
                    insertNote(child, word);
                    return;
                }    
            }
            
            newNode.getChildren().addAll(newChildren);
            treeNode.getChildren().removeAll(newChildren);
            treeNode.getChildren().add(newNode);
            newNode.setParent(treeNode);
            System.out.println("setting parent " + treeNode.getWord() + " to " + newNode.getWord());
        }
    }
    
    private String getWord(TreeNode treeNode, int depth) {
        System.out.println(treeNode.getWord() + " depth ---- " + depth);
            
        // ignore root node
        String longestWord = (depth > 0 && treeNode.getWord().length() == depth) ? treeNode.getWord() : "";
        String word = "";
        depth++;
        for(TreeNode child : treeNode.getChildren()) {
            word = getWord(child, depth);
            
            if(word.length() > longestWord.length())
                longestWord = word;
            else if (word.length() == longestWord.length()
                    && word.compareTo(longestWord) < 0)
                longestWord = word;
        }
        return longestWord;
    }
}

public class TreeNode {
    private String word;
    private TreeNode parent ;
    private List<TreeNode> children= new ArrayList<>();
    
    public TreeNode(){}
    
    public TreeNode(String word) {
        this.word = word;
    }
    
    public void addChild(TreeNode child) {
        children.add(child);
    }
    
    public List<TreeNode> getChildren() {
        return children;
    }
    
    public void setParent(TreeNode parent) {
        this.parent = parent;
    }
    
    public TreeNode getParent() {
        return parent;
    }
    
    public String getWord() {
        return word;
    }
}
```

# Solution 1 performance improve
1. root node always be length 1
2. after added order set, we only add children, no need for parent node.

```
class Solution {
    private TreeNode wordTree = new TreeNode();
    
    public String longestWord(String[] words) {
        // avoid duplicate words
        Set<String> wordSet = new TreeSet<>();
        wordSet.addAll(Arrays.asList(words));
        System.out.println(wordSet);
        for(String word : wordSet) {
            buildTree(word);
        }
        
        return getWord(wordTree, 0);
    }
    
    private void buildTree(String word) {
        if(word.length() == 1) {
            // the first node should be always 1 length
            wordTree.addChild(new TreeNode(word));
        }
        else {
            
            for(TreeNode child : wordTree.getChildren()) {
                System.out.println(child.getWord() + "-------" + word);
                if(word.startsWith(child.getWord())) {
                    insertNote(child, word);
                    break;
                }
            } 
        }    
       
    }
    
    private void insertNote(TreeNode treeNode, String word) {
        TreeNode newNode = new TreeNode(word);
        if (treeNode.getChildren().isEmpty()) {
             System.out.println("setting child " + newNode.getWord() + " to " + treeNode.getWord());
            treeNode.addChild(newNode);
        }
        else {
            // word starts with treeNode.getword
            List<TreeNode> newChildren = new ArrayList<>();
            for(TreeNode child : treeNode.getChildren()) {
                if(word.startsWith(child.getWord())) {
                    insertNote(child, word);
                    return;
                }    
            }
            
            //new node is a child or current tree node
            treeNode.getChildren().add(newNode);
            System.out.println("setting parent " + treeNode.getWord() + " to " + newNode.getWord());
        }
    }
    
    private String getWord(TreeNode treeNode, int depth) {
        System.out.println(treeNode.getWord() + " depth ---- " + depth);
            
        // ignore root node
        String longestWord = (depth > 0 && treeNode.getWord().length() == depth) ? treeNode.getWord() : "";
        String word = "";
        depth++;
        for(TreeNode child : treeNode.getChildren()) {
            word = getWord(child, depth);
            
            if(word.length() > longestWord.length())
                longestWord = word;
            else if (word.length() == longestWord.length()
                    && word.compareTo(longestWord) < 0)
                longestWord = word;
        }
        return longestWord;
    }
}

public class TreeNode {
    private String word;
    private List<TreeNode> children= new ArrayList<>();
    
    public TreeNode(){}
    
    public TreeNode(String word) {
        this.word = word;
    }
    
    public void addChild(TreeNode child) {
        children.add(child);
    }
    
    public List<TreeNode> getChildren() {
        return children;
    }
    
    public String getWord() {
        return word;
    }
}
```
