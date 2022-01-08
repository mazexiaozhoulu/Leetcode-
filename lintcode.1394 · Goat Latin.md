```
class Solution:
    """
    @param S: 
    @return: nothing
    """
    def  toGoatLatin(self, S):
        vowel=set("aeiouAEIOU")
        word=[]
        latin=" "
        for i,w in enumerate(S.split()):
            if w[0] not in vowel:
                word.append(w[1:]+w[0]+"ma"+"a"*(i+1))
            else:
                word.append(w+"ma"+"a"*(i+1))
    
        GoatLatin=latin.join(word)
        return GoatLatin
```
