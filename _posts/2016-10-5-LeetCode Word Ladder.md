---
layout: post
title: LeetCode-Word ladder 1
---

> Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:
> Only one letter can be changed at a time
> Each intermediate word must exist in the word list
> For example,

> Given:
> beginWord = "hit"
> endWord = "cog"
> wordList = ["hot","dot","dog","lot","log"]
> As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
> return its length 5.

> Note:
> Return 0 if there is no such transformation sequence.
> All words have the same length.
> All words contain only lowercase alphabetic characters.


-----

刚开始看到之后根本无从下手，看了别人的思路才知道是用图解决。如果两个单词只差一个字母，相当于两个单词之间有连线。即求start到end的最短路径长度。
用BFS做比较合适。

	public class Solution {

		
		
		public int ladderLength(String start, String end, Set<String> dict) {
			
			Queue<WordNode> queue = new LinkedList<WordNode>();
			queue.add( new WordNode(start, 1) );
			
			dict.add(end);
			
			
			while ( !queue.isEmpty() ) {
				
				WordNode top = queue.remove();
				String word = top.word;
				
				if ( word.equals(end) )
					return top.steps;
				
				char[] arr = word.toCharArray();
				
				for (int i = 0; i < arr.length; i++) {
					
					for (char ch = 'a'; ch <= 'z'; ch++) {
						
						char temp = arr[i];
						if ( ch != arr[i] ) {
							arr[i] = ch;
						}
						
						String newWord = new String(arr);
						if (dict.contains(newWord)) {
							queue.add( new WordNode(newWord, top.steps + 1) );
							dict.remove(newWord);
						}
						
						arr[i] = temp;
					}
				}
			}
			
			return 0;
			
		}
		
		
		
		
		
		class WordNode {
			String word;
			int steps;
			
			public WordNode(String word, int steps) {
				
				this.word = word;
				this.steps = steps;
			}
		}
		
	}
