# ST2334 Probability And Statistics 

## Tutorial 1 
1) a) P(both cities) = P(A) + P(B) - P(either city)
        0.7 + 0.4 - 0.8 = 0.3
    b) P(neither city) = 1 - P(either city) 
        1 - 0.8 = 0.2
   
2) a) C(30,5) = 142,506
    b) P(no minority candidates) = 23/30 * 22/29 * 21/28 * 20/27 * 19/26 
	= 0.23612 (4.s.f)
    c) P(no more than 1) = P(no minority) + P(only 1)
	= 0.6711 (4.s.f)

3) a) P(A) = 13/52 * 12/51 * 11/50 * 10/49 * 9/48 * 4
	= 0.001981 (4s.f)
	OR
	13C5 * 4 / 52C5
    b) Total 5 card hands = 52C5 = 2598960
	10 * 4 * 4 * 4 * 4 * 4 - 40 / 2598960
 
4) a) P(both lights) = P(first) + p(second) - p(at least 1)
	= 0.4 + 0.5 - 0.6 = 0.3
    b) P(exactly one) = 1 - P(both) - P(none)
	= 1 - 0.3 - (1 - 0.6) = 0.7 - 0.4 = 0.3
    c) P(neither) = 1 - P(exactly 1) - P(both)
	= 1 - 0.3 - 0.3 = 0.4
    d) P(second | first) = P(first and second) / P(first)
	= 0.3 / 0.4 = 0.75
    e) P(both lights) = 0.3
	P(A) * P(B) = 0.2
	Since they are not equal they are not independent events
   
5) a) First digit cannot be zero, can only choose n - 1 digits to avoid choosing the prev digit
	9 * 9<sup>8</sup> / 9 * 10<sup>8</sup> = 0.430
	 
    b) Choose 3 digits out of 8 slots, then fill remaining with any except 0
	8C3 * 9<sup>3</sup> /  9 * 10<sup>8</sup> = 0.0331
   
   
6) a) P(nonconforming) = 0.01 + 0.025
	= 0.035
    b) P(filled on II) = 0.5
    c) P(machine II and conforming) = P(machine II) - P(machine II and not conforming)
	= 0.5 - 0.025 = 0.475
    d) P(machine I or is a conforming bottle) = P(conforming) + P(machine 1 and not conforming)
	= P(machine I) + P(conforming bottle) - P(machine I and is a conforming bottle)
	= 0.5 + 0.965 -  (P(machine I) - P(machine 1 and not conforming))
	= 0.965 + 0.01
	= 0.975
    e) P(nonconforming | I) = P(I and nonconforming) / P(I)
	0.01 / 0.5 = 0.02
    f) P(I | nonconforming) = P(I and nonconforming) / P(nonconforming)
	= 0.01 / 0.035 = 0.2857 (4s.f)
    g)