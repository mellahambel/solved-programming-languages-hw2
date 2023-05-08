Download Link: https://assignmentchef.com/product/solved-programming-languages-hw2
<br>
You will write 11 SML functions (not counting local helper functions), 4 related to “name substitutions” and 7 related to a made-up solitaire card game.

Your solutions must use pattern-matching. You may not use the functions null, hd, tl, isSome, or valOf, nor may you use anything containing a # character or features not used in class (such as mutation). Note that list order does not matter unless specifically stated in the problem.

<em>Download hw2provided.sml from the course website. </em>The provided code defines several types for you. You will not need to add any additional datatype bindings or type synonyms.

The sample solution, not including challenge problems, is <em>roughly </em>130 lines, including the provided code.

Do not miss the “Important Caveat” and “Assessment” after the “Type Summary.”

<ol>

 <li>This problem involves using first-name substitutions to come up with alternate names. For example, <em>Fredrick William Smith </em>could also be <em>Fred William Smith </em>or <em>Freddie William Smith</em>. Only part (d) is specifically about this, but the other problems are helpful.</li>

</ol>

<ul>

 <li>Write a function all_except_option, which takes a string and a string list. Return NONE if the string is not in the list, else return SOME <em>lst </em>where <em>lst </em>is identical to the argument list except the string is not in it. You may assume the string is in the list at most once. Use same_string, provided to you, to compare strings. Sample solution is around 8 lines.</li>

 <li>Write a function get_substitutions1, which takes a string list list (a list of list of strings, the <em>substitutions</em>) and a string <em>s </em>and returns a string list. The result has all the strings that are in some list in <em>substitutions </em>that also has <em>s</em>, but <em>s </em>itself should not be in the result. Example:</li>

</ul>

get_substitutions1([[“Fred”,”Fredrick”],[“Elizabeth”,”Betty”],[“Freddie”,”Fred”,”F”]],

“Fred”)

<ul>

 <li>answer: [“Fredrick”,”Freddie”,”F”] *)</li>

</ul>

Assume each list in <em>substitutions </em>has no repeats. The result will have repeats if <em>s </em>and another string are both in more than one list in <em>substitutions</em>. Example:

get_substitutions1([[“Fred”,”Fredrick”],[“Jeff”,”Jeffrey”],[“Geoff”,”Jeff”,”Jeffrey”]],

“Jeff”)

(* answer: [“Jeffrey”,”Geoff”,”Jeffrey”] *)

Use part (a) and ML’s list-append (@) but no other helper functions. Sample solution is around 6 lines.

<ul>

 <li>Write a function get_substitutions2, which is like get_substitutions1 except it uses a tail-recursive local helper function.</li>

 <li>Write a function similar_names, which takes a string list list of substitutions (as in parts (b) and (c)) and a <em>full name </em>of type {first:string,middle:string,last:string} and returns a list of full names (type {first:string,middle:string,last:string} list). The result is all the full names you can produce by substituting for the first name (and <em>only the first name</em>) using <em>substitutions </em>and parts (b) or (c). The answer should begin with the original name (then have 0 or more other names). Example:</li>

</ul>

similar_names([[“Fred”,”Fredrick”],[“Elizabeth”,”Betty”],[“Freddie”,”Fred”,”F”]], {first=”Fred”, middle=”W”, last=”Smith”})

<ul>

 <li>answer: [{first=”Fred”, last=”Smith”, middle=”W”},</li>

</ul>

{first=”Fredrick”, last=”Smith”, middle=”W”},

{first=”Freddie”, last=”Smith”, middle=”W”},

{first=”F”, last=”Smith”, middle=”W”}] *)

Do not eliminate duplicates from the answer. Hint: Use a local helper function. Sample solution is around 10 lines.

<ol start="2">

 <li>This problem involves a solitaire card game invented just for this question. You will write a program that tracks the progress of a game; writing a game player is a challenge problem. You can do parts (a)–(e) before understanding the game if you wish.</li>

</ol>

A game is played with a <em>card-list </em>and a <em>goal</em>. The player has a list of <em>held-cards</em>, initially empty. The player makes a move by either <em>drawing</em>, which means removing the first card in the card-list from the card-list and adding it to the held-cards, or <em>discarding</em>, which means choosing one of the held-cards to remove. The game ends either when the player chooses to make no more moves or when the sum of the values of the held-cards is greater than the goal.

The objective is to end the game with a low score (0 is best). Scoring works as follows: Let <em>sum </em>be the sum of the values of the held-cards. If <em>sum </em>is greater than <em>goal</em>, the <em>preliminary score </em>is three times (<em>sum</em>−<em>goal</em>), else the preliminary score is (<em>goal </em>− <em>sum</em>). The score is the preliminary score unless all the held-cards are the same color, in which case the score is the preliminary score divided by 2 (and rounded down as usual with integer division; use ML’s div operator).

<ul>

 <li>Write a function card_color, which takes a card and returns its color (spades and clubs are black, diamonds and hearts are red). Note: One case-expression is enough.</li>

 <li>Write a function card_value, which takes a card and returns its value (numbered cards have their number as the value, aces are 11, everything else is 10). Note: One case-expression is enough.</li>

 <li>Write a function remove_card, which takes a list of cards cs, a card c, and an exception e. It returns a list that has all the elements of cs except c. If c is in the list more than once, remove only the first one. If c is not in the list, raise the exception e. You can compare cards with =.</li>

 <li>Write a function all_same_color, which takes a list of cards and returns true if all the cards in the list are the same color. Hint: An elegant solution is very similar to one of the functions using nested pattern-matching in the lectures.</li>

 <li>Write a function sum_cards, which takes a list of cards and returns the sum of their values. <em>Use a locally defined helper function that is tail recursive. (Take “calls use a constant amount of stack space” as a requirement for this problem.)</em></li>

 <li>Write a function score, which takes a card list (the held-cards) and an int (the goal) and computes the score as described above.</li>

 <li>Write a function officiate, which “runs a game.” It takes a card list (the card-list) a move list (what the player “does” at each point), and an int (the goal) and returns the score at the end of the game after processing (some or all of) the moves in the move list in order. Use a locally defined recursive helper function that takes several arguments that together represent the current state of the game. As described above:

  <ul>

   <li>The game starts with the held-cards being the empty list.</li>

   <li>The game ends if there are no more moves. (The player chose to stop since the move list is empty.)</li>

   <li>If the player discards some card c, play continues (i.e., make a recursive call) with the held-cards not having c and the card-list unchanged. If c is not in the held-cards, raise the IllegalMove</li>

   <li>If the player draws and the card-list is (already) empty, the game is over. Else if drawing causes the sum of the held-cards to exceed the goal, the game is over (after drawing). Else play continues with a larger held-cards and a smaller card-list.</li>

  </ul></li>

</ul>

Sample solution for (g) is under 20 lines.

<ol start="3">

 <li><strong>Challenge Problems:</strong></li>

</ol>

<ul>

 <li>Write score_challenge and officiate_challenge to be like their non-challenge counterparts except each ace can have a value of 1 or 11 and score_challenge should always return the least (i.e., best) possible score. (Note the game-ends-if-sum-exceeds-goal rule should apply only if there is no sum that is less than or equal to the goal.) Hint: This is easier than you might think.</li>

 <li>Write careful_player, which takes a card-list and a goal and returns a move-list such that calling officiate with the card-list, the goal, and the move-list has this behavior:

  <ul>

   <li>The value of the held cards never exceeds the goal.</li>

   <li>A card is drawn whenever the goal is more than 10 greater than the value of the held cards. As a detail, you should (attempt to) draw, even if no cards remain in the card-list.</li>

   <li>If a score of 0 is reached, there must be no more moves.</li>

   <li>If it is possible to reach a score of 0 by discarding a card followed by drawing a card, then this must be done. Note careful_player will have to look ahead to the next card, which in many card games is considered “cheating.” Also note that the previous requirement takes precedence: There must be no more moves after a score of 0 is reached even if there is another way to get back to 0.</li>

  </ul></li>

</ul>

Notes:

<ul>

 <li>There may be more than one result that meets the requirements above. The autograder should work for any correct strategy — it checks that the result meets the requirements.</li>

 <li>This problem is <em>not </em>a continuation of problem 3(a). In this problem, all aces have a value of 11.</li>

</ul>

<h1>Type Summary</h1>

Evaluating a correct homework solution should generate these bindings, in addition to the bindings from the code provided to you — <em>but see the important caveat that follows.</em>

val all_except_option = fn : string * string list -&gt; string list option val get_substitutions1 = fn : string list list * string -&gt; string list val get_substitutions2 = fn : string list list * string -&gt; string list val similar_names = fn : string list list * {first:string, last:string, middle:string}

-&gt; {first:string, last:string, middle:string} list val card_color = fn : card -&gt; color val card_value = fn : card -&gt; int val remove_card = fn : card list * card * exn -&gt; card list val all_same_color = fn : card list -&gt; bool val sum_cards = fn : card list -&gt; int val score = fn : card list * int -&gt; int val officiate = fn : card list * move list * int -&gt; int

<h1>Important Caveat</h1>

The REPL may give your functions <em>equivalent types </em>or <em>more general </em>types. This is fine. In the sample solution, the bindings for problems 1d, 2a, 2b, 2c, and 2d were all more general. For example, card_color had type suit * ’a -&gt; color and remove_card had type ’’a list * ’’a * exn -&gt; ’’a list. They are more general, which means there is a way to replace the <em>type variables </em>(’a or ’’a) with types to get the bindings listed above. As for equivalent types, because type card = suit*rank, types like card -&gt; int and suit*rank-&gt;int are equivalent. They are the same type, and the REPL simply chooses one way of printing the type. Also, the order of fields in records never matters.

If you write down explicit argument types for functions, you will probably not see equivalent or more-general types, but we encourage the common ML approach of omitting all explicit types.

Of course, generating these bindings does not guarantee that your solutions are correct. <em>Test your functions: Put your testing code in a second file. We will not grade the testing file, nor will you turn it in, but surely you want to run your functions and record your test inputs in a file.</em>

<h1>Assessment</h1>

We will automatically test your functions on a variety of inputs, including edge cases. We will also ask peers to evaluate your code for simplicity, conciseness, elegance, and good formatting including indentation and line breaks. Your solution will also be checked for using only features discussed so far in class, and to ensure that it does not use any of the banned features listed at the beginning of the assignment, such as hd and #foo.