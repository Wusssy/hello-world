# String_index_KMP

def kmp_match(s, p):
    ls = len(s)
    lp = len(p)
    start = 0
    table = partial_table(p)
    while start <= ls-lp:
        for i in range(lp):
            if s[i+start] != p[i]:
                start += max(i-table[i-1], 1)
                break
            else:
                return True
    return False


def partial_table(p):
    prefix = set()
    postfix = set()
    res = [0]
    for i in range(1, len(p)):
        prefix.add(p[:i])
        postfix = {p[j:i+1] for j in range(1, i+1)}
        res.append(len((prefix & postfix or {''}).pop()))
    return res
    
  
print(partial_table("ABCDABD"))
print(kmp_match("BBC ABCDAB ABCDABCDABDE", "ABCDABD"))
