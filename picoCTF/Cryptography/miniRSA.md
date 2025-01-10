# miniRSA
this challenge is based on RSA Cryptosystem. In this we are given the values of product of prime numbers p and q `n`, exponent `e` and ciphertext `c`.
From this information we have to find the encrypted message `m`. 
The values of `n`,`e` and `c` is given here :- `https://mercury.picoctf.net/static/a24cf907007a19dbf30310acad0df9e5/ciphertext`.

If we take a look at this, we see that the value of `e` is very small, which is 3. Now, we know that `c = m**e % n`, if `m**e` < `n` then `c = m**e`.
Which is the case here. Therefore to find `m` might have to find the value of cube root of `c`.
And then check if `m**3` is equal to `c` or not. initially I tried finding the value of `m` using online tools, but I was not getting the correct result. This was because
after getting the value of `m`, I converted it to hexadecimal and then ASCII to see if the message is a readable or not. I got some garbage ASCII text.

Then, It might be possible that `m**e = c + i*n`, where c is a constant. To find this the program for it is given below:-
```bash
from Crypto.Util.number import long_to_bytes

def find_invpow(x,n):
    """Finds the integer component of the n'th root of x,
    an integer such that y ** n <= x < (y + 1) ** n.
    """
    high = 1
    while high ** n < x:
        high *= 2
    low = high // 2
    while low < high:
        mid = (low + high) // 2
        if low < mid and mid**n < x:
            low = mid
        elif high > mid and mid**n > x:
            high = mid
        else:
            return mid
    return mid + 1

c = 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808145893251774383242888588567652079502880522005531571120463301333725071534050137246298274874319432561063978068140428652193294702808687000503934999928337234367205234422580586283326017530708854836817980318398277272759022724136418545105867685463283579824831916699431331460258806680372323026200534791012439563034432826050072742892112790177234284090476467119938191076883854821999876464545771711445501514467804193760659882386680300508589975451301720477703627085437101600726487172968870448635983769708507451946168500510817590720157574816563284526466526806699820426206566718022595284382939272542309819250701217431454132436646725890151031992160610219312035760562959174778547776304922277751548955049884940378
e = 3
n = 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
i = 0
flag = 1 # this variable is used as a counter variable in the while loop to make it always true.

while flag == 1:
    string = long_to_bytes(find_invpow(c + i*n,e))
    if b'picoCTF' in string:
        print(string)
        print(i)
        break
    i = i + 1
```

The program to find the cube root I go from here:- `https://stackoverflow.com/questions/55436001/cube-root-of-a-very-large-number-using-only-math-library`.
After that a values to `c`, `n`, and `e` are assigned. I is the contant here which is initialized to 0 at the beginning and a variable `flag` is used
to make the condition inside while loop always true. Now to use the function `long_to_bytes` first we have to install the `pycryptodome` package which has 
`Crypto.Util.number` library and from there we import `long_to_bytes`. I assigned the variable `string` to the hex value of the cube root we find from the
function `find_invpow`. An if statement is used such that it prints `string` as it finds `pico` in `string` and also it prints `i` where it is present and then
we break out of the loop as soon as we find the word `picoCTF`.

The terminal output is given below:-
```bash
PS C:\Users\Muizz Ahmed> python -u "\\wsl.localhost\Ubuntu-22.04\home\muizz\miniRSA.py"
b'                                                                                                        picoCTF{e_sh0u1d_b3_lArg3r_0b39bbb1}'
3533
PS C:\Users\Muizz Ahmed>
```

## References
1.) `https://picoctf.org/learning_guides/Book-2-Cryptography.pdf`
2.) `https://en.wikipedia.org/wiki/RSA_(cryptosystem)`
##
#
