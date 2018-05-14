# Leetcode: Dota2 Senate     :BLOG:Basic:


---

Dota2 Senate  

---

Similar Problems:  
-   Tag: [#game](https://code.dennyzhang.com/tag/game), [#greedy](https://code.dennyzhang.com/tag/greedy), [#inspiring](https://code.dennyzhang.com/tag/inspiring)

---

In the world of Dota2, there are two parties: the Radiant and the Dire.  

The Dota2 senate consists of senators coming from two parties. Now the senate wants to make a decision about a change in the Dota2 game. The voting for this change is a round-based procedure. In each round, each senator can exercise one of the two rights:  

-   Ban one senator's right:

A senator can make another senator lose all his rights in this and all the following rounds.  

-   Announce the victory:

If this senator found the senators who still have rights to vote are all from the same party, he can announce the victory and make the decision about the change in the game.  
Given a string representing each senator's party belonging. The character 'R' and 'D' represent the Radiant party and the Dire party respectively. Then if there are n senators, the size of the given string will be n.  

The round-based procedure starts from the first senator to the last senator in the given order. This procedure will last until the end of voting. All the senators who have lost their rights will be skipped during the procedure.  

Suppose every senator is smart enough and will play the best strategy for his own party, you need to predict which party will finally announce the victory and make the change in the Dota2 game. The output should be Radiant or Dire.  

Example 1:  

    Input: "RD"
    Output: "Radiant"
    Explanation: The first senator comes from Radiant and he can just ban the next senator's right in the round 1.
    And the second senator can't exercise any rights any more since his right has been banned.
    And in the round 2, the first senator can just announce the victory since he is the only guy in the senate who can vote.

Example 2:  

    Input: "RDD"
    Output: "Dire"
    Explanation:
    The first senator comes from Radiant and he can just ban the next senator's right in the round 1.
    And the second senator can't exercise any rights anymore since his right has been banned.
    And the third senator comes from Dire and he can ban the first senator's right in the round 1.
    And in the round 2, the third senator can just announce the victory since he is the only guy in the senate who can vote.

Note:  
-   The length of the given string will in the range [1, 10,000].

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/dota2-senate)  

Credits To: [leetcode.com](https://leetcode.com/problems/dota2-senate/description/)  

Leave me comments, if you have better ways to solve.  

    // Blog link: https://code.dennyzhang.com/dota2-senate
    // Basic Ideas: greedy
    //
    //  Each senator ban the next closet opponent senator
    //
    //  Two queue: queue_r, queue_d
    //      Put all indices
    //      Remove them
    //      Check which queue has more element
    //
    // Complexity: Time O(n), Space O(n)
    func predictPartyVictory(senate string) string {
        n := len(senate)
        queue_r, queue_d := []int{}, []int{}
        for i, ch := range senate {
            if ch == 'R' { 
                queue_r = append(queue_r, i) 
            } else {
                queue_d = append(queue_d, i) 
            }
        }
    
        for len(queue_r) > 0 && len(queue_d) > 0 {
            r_index, d_index := queue_r[0], queue_d[0]
            queue_r, queue_d = queue_r[1:], queue_d[1:]
            if r_index<d_index {
                queue_r = append(queue_r, r_index+n)
            } else {
                queue_d = append(queue_d, d_index+n)
            }
        }
        if len(queue_d) == 0 {
            return "Radiant"
        } else {
            return "Dire"
        }
    }