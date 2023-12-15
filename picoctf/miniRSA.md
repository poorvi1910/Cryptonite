We know that rsa formula is:
c=m^e mod n
So to find m, we take any random integer k, so m will be:
m=( k*n+c)^1/e
Hence we write the following python program which finds all the possible m values and prints the one which has the flag
-----------------------------------------------------------------------------------------------------------------------------
import Crypto.Util.number

#C = m^e mod n
#m^e=k*n +c


n=29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
c=2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141


def find_invpow(x,n):
    """Finds the integer component of the n'th root of x,
    an integer such that y ** n <= x < (y + 1) ** n.
    """
    high = 1
    while high ** n < x:
        high *= 2
    low = high//2
    while low < high:
        mid = (low + high) // 2
        if low < mid and mid**n < x:
            low = mid
        elif high > mid and mid**n > x:
            high = mid
        else:
            return mid
    return mid + 1

k=0
while True:
    m=Crypto.Util.number.long_to_bytes(find_invpow(k*n +c ,3))
    if b'pico'in m:
        print(m)
        break
    k+=1
-----------------------------------------------------------------------------------------------

Running the code we get : picoCTF{n33d_a_lArg3r_e_d0cd6eae}
