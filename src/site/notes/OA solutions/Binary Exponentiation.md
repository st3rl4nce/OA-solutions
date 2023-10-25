---
{"dg-publish":true,"permalink":"/oa-solutions/binary-exponentiation/"}
---

# What does it solve in general?
* Consider the problem of finding $a^n$ for $a, n {\in} \mathbb{N}$.
* If we were to go with the usual approach of finding it, we'd be going through $n$ multiplications on the total, which ain't bad, but is not feasible for $n {\ge} 10^8$. Also multiplication is an expensive operation in general, and is preferable to reduce the no. of operations whenever possible.
* Binary exponentiation improves this to $O(logn)$ multiplications on the whole, which is a significant improvement over $n$, implying we can find or use powers of $a$ for as great as $n = 10^{10^8}$.

# Intuition
* The central idea of binary exponentiation is pretty simple, given an $n$, we can express it in it's binary form, which is nothing but $2^{p_1}+2^{p_2}+...+2^{p_k}$, now we know that $n^{m_1+m_2} = n^{m_1}*n^{m_2}$.
* Now, equivalently we can express $a^n$ as $a^{2^{p_1}}*a^{2^{p_2}}*...*a^{2^{p_k}}$, ${p_1}<{p_2}<...{p_k}$.
* Now, coming to the powers of $a$, we can express $a^2=a^1*a^1, a^4 = a^2*a^2$, and so on. 
* So now, coming to expressing $n$ in binary, let's take an example, say, $n=29, = 11101 = 2^4+2^3+2^2+2^0$, so $a^n = a^{2^4}*a^{2^3}*a^{2^2}*a^{2^0}$.
* Here, we can observe that $a^{2^3} == a^{2^2}*a^{2^2}$, so basically, we want to find is $a^n = a^{2^4}*a^{2^3}*a^{2^2}*a^{2^0}$, and if we were to consider the binary representation, we're just multiplying our result with $a^{2^{pos}}$, whenever the bit at $pos$ is set.
* Now all we have to do is find all  $a^{2^{p_i}}$, involved and multiply them, which can be done in $p_i$ multiplications, since $a^{2^{p_i}} == a^{2^{p_{i-1}}}*a^{2^{p_{i-1}}}$.
* Now in the process of finding $p_k$, we will come across all other $p_i$'s, so we can just multiply them to the result in the process itself, whenever the bit is set.

# Algorithm
* It is pretty evident from intuition that all we have to do is iterate the binary representation of $n$, while finding the powers of $a$, and whenever we find the current bit is set multiply the result with that power of $a$.
* Formally, 
	* iterate the bitset of $n$ from left to right, in the process also find the power of $a$ till the no.of elements of bitset from the left have been covered till then.
	* If the bit is set, then multiply the current power of $a$ stored in $a$ with $res$.
* Code (C++)
```
	int pow(int a, int n){
		int res = 1;
		while(n>0){
			// check if the least significant bit is set
			if(n&1)
				res*=a;
			%% by multiplying a with a, we get a^2, which implies if a currently stores a^p, then in the next iteration it has a^p+1, which is in line with out algo, since we're checking for set bits from the least significant(p0) to the most significant(pk) %%
			a*=a;
			res>=1;
		}
		return res;
	}
```

