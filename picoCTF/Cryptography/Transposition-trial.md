# Transposition Trial

The challenge desciption provides us with a text file which the folowing message :- 
`heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V9AAB1F8}7`
and we have to decode this message

## Hint
1.) Split the message up into blocks of 3 and see how the first block is scrambled
##

After splitting in groups of 3, we get the following:-
`heT,fl ,g a,s i,icp,CTo,{7F,4NR,P05,1N5,_16,_35,P3X,51N,3_V,9AA,B1F,8}7`. We also have to include space as a member of the group to get the right answer.
As we can see that the 3rd element of the group should be in 1st, 1st should be in 2nd and finally 2nd should be in 3rd.
Now, after decoding it we get the following message
`The flag is picoCTF{7R4N5P051N6_15_3XP3N51V3_A9AFB178}`

FLAG:- `picoCTF{7R4N5P051N6_15_3XP3N51V3_A9AFB178}`

This is how i solved it.
#
