'''
In the United Kingdom the currency is made up of pound (£) and pence (p). There are eight coins in general circulation:

1p, 2p, 5p, 10p, 20p, 50p, £1 (100p), and £2 (200p).
It is possible to make £2 in the following way:

1×£1 + 1×50p + 2×20p + 1×5p + 1×2p + 3×1p
How many different ways can £2 be made using any number of coins?
'''


'''
im going to do this by solving the general solution and then plugging in 2.

notes:
- for each coin, were going to have to recurse for each amount of times that we can remove the current coin from the sum, onto the remainder. thats actactually the solution.
- doesnt really matter the order we do this, since we have to do all possibilities of all coins.
- we should also memoize the solution but luckily we only ned to apply this to 2
- were going to standardize all the coins to work with p only.
- this problem is suuupper close to being a problem of generating all permutatinos. this problem may be a generalization of permutations. maybe permutations would be a special case where every item equally reduces amount before recursing.

solution:

given an amount, in pence, and the set of coins, we will loop over the amount of ways we can take the current coin, and we will recurse into the subproblem that is a consequence of taking those coins.

we have to return the amount of ways that we can traverse this recursion. so i will maintain a count of the amount of times we reach a valid base case and return that.

algo:

counter = 0

c(ith coin,amount):
  if amount = 0:
    counter += 1
  #elif amount - ith coin == 0:  #this could end up being the same condition as above depending on how we recurse
  else:
    remainder = amount
    #while we CAN pick the current coin, do so and recurse
    while remainder > ith coin:
      c(i+1, remainder - number of times ith coin picked)
    #the recursion c(i+1,remainder-0) is crucial in ensuring that we try every possible combination

edge cases: there are no more coins to try
'''

'''
eg:
c(6,200):
  recurse:
    p=0
    c=100
    ---
    0*100 <=  200:
    c(7,200):
      recurse:
        p=0
        coin=200
        ---
        0*200 <= 200:
        c(8,200): break
        p=1
        ---
        1*200 <= 200:
        c(8,0): counter + 1 #this is good, its something we needed to confirm
        p=2
        ---
        2*200 <= 200 is false
        break
    p=1
    ---
    1*100 <= 200:
    c(7,100):
      recurse: nothing happens because cant get to 100 using 200s
    p=2
    ---
    2*100 <= 200:
    c(7,0): counter+=1
    p=3
    ---
    3*100 <= 200 is false
    break

lets memoize: if we're at a specific coin with a specific amount, we should know how many possible ways there are to achieve this subproblem already. we should probably work with returns then.

'''

pences = [1, 2, 5, 10, 20, 50, 100, 200]

memo = {i:{} for i in range(len(pences)+1)}

def c(i,amount):
  if amount == 0:
    return 1
  elif i < len(pences):
    picks=0
    coin=pences[i]
    num_ways = 0
    while picks*coin <= amount:
      remainder = amount-picks*coin
      if memo[i+1].get(remainder,None) is None:
        memo[i+1][remainder] = c(i+1,remainder)
      num_ways += memo[i+1][remainder]
      picks += 1
    memo[i][amount] = num_ways
    return memo[i][amount]
  else:
    return 0

c(0,200)

print(memo[0][200])
