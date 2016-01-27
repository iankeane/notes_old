Ian Keane

---------------------
Computational Science
---------------------


Tue Jan 12 09:24:10 EST 2016
---------------------------------------------------------

Notes at: cyn.help/CS/Scientific


What is Scientific Computing
    taking the limited scope of the computer and emulating what a human
        could do with infinite resources
    computers are limited in that they cannot understand concepts like
        infinity

Numbers
    rational - Q
        def: n/m where n is in Z
    irrational
        def: n/m where n is not in Z but n/m is in R
    integers - Z
    floating point
    count positive integers - Z+
    non-negative (natural) - N
    prime
    real - R
        def: !!!
    complex - C
    even (includes zero)
        def: x%0=0 or x=2k when k is in Z
    odd
        def: x=2k+1 when k is in Z
    zero is non-positive and non-negative
Intervals
    closed interval
        ex: [1,10]
        1,2,...,9,10
    open interval
        ex: (1,10)
        2,3,...,8,9
    interval brackets can also be mixed

Functions takes an input and returns an output
        ex: f(x)=x
        takes x and returns x
        typically f:R->R
    continuous functions
        defined at every point in a domain
        no discontinuities
        unbounded or continuous in bounds
    computers cannot calculate continuous functions
        cannot handle infinite bounds or infinite distance between
            numbers
        can only make approximations
        ex: jpeg zooming causes pixillation
Integers
    alphabet
        digits: 0,1,...,8,9 
    operators
        + addition
        * multiplication
        ^ exponentiation
    defining 1024 in decimal
        1024=1*10^3+0*10^2+2*10^1+4*10^0
    defining 1024 in binary
        
Using 1 and 0
    can be thought of as a switch [on,off]
        can also represent electrical current
    alphabet
        digits: 0,1
    operators
        0+0=0 | 0*0=0
        0+1=1 | 0*1=0
        1+1=0 | 1*0=0
        1+1=0 | 1*1=1
    

Thu Jan 14 09:30:00 EST 2016
---------------------------------------------------------

Numbers and Bases
    all numbers can be broken down as above
    the number being raised to the exponent is called the base
        each additional digit represents another degree of freedom
        base 10 digits: 1-9
            ex: 101 = 1*10^2+0*10^1+1*10^0 = 101
        base 2 digits: 0-1
            ex: 101 = 1*2^2+0*2^1+1*2^0 = 5
            these examples are called expansions 
        rewriting 1024(base 60) in base 10:
            1*60^4+0*60^3+2*60^1+1*60^0

Bit Architectue
    an eight bit machine allows 8 bits in binary
        i.e. the highest number is 11111111 = 255
        this is 256 digits (counting zero)
    during the cold war, the russians tried to create trinary computers
        using positive, negative, and zero
        this was too fuzzy, caused the idea to fail
    hexidecimal can be understood quickly by computers and hold larger numbers
        this is base 16
        it can be easily translated into binary
        uses digits 0,...,9 and a,...,f
        255 can be represented in two digits as ff
        thus hexidecimal can store all 8-bit numbers in two digits
    how to convert hex to binary (easily)
        ex: 59 in binary is 111011
            1. make 8 digits
                00111011
            2. separate into groups of four
                0011 1011
            3. translate both to hex
                3 b
            4. concatenate
                3b
    we can store color in values of 255
        this is what we mean by "8 bit color"
        we can also write this in hex (ff)
        we do not raise the base further, because it would not help
        this is because the next base up is base 255, which is the same as 0-255
            in base 10
    octal (base 8) can also be used to save some space
        uses digits 0,...,7
        less efficient than base ten, but almost as efficient
        considered attractive in the 90's because of it's closeness to base 10
        this makes it easier to convert using expansions
        conversion to octal (without expansions)
            ex: 59 in binary is 11011
                1. add necessary zeros
                    011011
                2. separate into groups of three
                    011 011
                3. translate all to octal 
                    7 3
                4. concatenate
                    73
    base 4 does not contribute significant savings


Tue Jan 19 09:52:46 EST 2016  
----------------------------  

Representing Decimals in Binary  
    in any expansion, the decimal can be representing by confinuing to 10^-1  
        ex: 1*10^1+1*10^0+1*10^-1+1*10^-2 = 11.11  
    !!! do binary  

Floating Points  
    rational numbers with fixed maximum places  
        ex: 2/3 = .66(repeating) = .6667  
        error = abs(2/3 - .6667) = abs(2-3(.6667)) = .0001 = 10^-4  
    the precision is the number of significant digits we can store  
        ex: 1/64 can not be accurately stored at 10^-4 precision  
        error is 2.5*10^-5  

Floating Points and Scientific Notation  
    ex: 12.345 = 1.2345*10^1 = 12345*10^-3  
        12345 is the mantissa  
        mantissa begins and ends with a nonzero number  
        three parts to this, the mantissa, the base, and the exponent, and sign  
        these parts are stored in fixed bits  
    we can encode this number with the point at any place  
        this is why the data structure is called a "floating point"  
    the standard used for this is called IEEE 754  

Storing Floating Points  
    to store this in a 32-bit register (IEEE 754):  
        use one bit for sign (+ or -)  
        8 bits for the exponent  
        remaining bits for mantissa  
        no bits needed for base, because it is always base 2  
    # of bits allocated to the exponent tell us how big the number can be  
    # of bits allocated to the mantissa tell us the precision  
        by IEEE standard, 64-bit systems have 11 bits for exponent, 52 for  
            the mantissa  
    the exponent can go from 0-256, but has no sign  
        if we have no sign for the exponent, we can not store fractions  
        to solve this, half of the numbers 0-255 represent negative, half  
            positive numbers  
        0-127 = negative, 127-255 = positive  
            this is achieved by subtracting 127 from the exponent stored  
        exponent can go up to 128  
    to store the mantissa:  
        because the mantissa is only significant digits, we know the first  
            digit will be 1 in base 2, so we don't store the first bit  
        store the mantissa without the leading one  
        stored with most significant digit on the right, least on the left  
            ex: 5.375 
                is 101.011 in binary 
                    mantissa is 01011  
                    exponent is -3  
                exponent is -3  
                    stored as 255-127-3 = 124 = 0111 1101 
                0 0111110 001011 
            pad on the right (we can do this because we are representing
                fractions at this point)
        
Note on 32 and 64 bit  
    this denotes number of bits used to store a number  
        each memory register has 32 or 64 bits  
        on 32-bit, we can store 2^32 different numbers  
    cpu has to be referenced at each byte  
        32-bit system can only keep up with 4-gigabytes at a time  

Exponential Math Note  
    2^10 = 1024  
    2^20 = 1024^2  
    2^32 = (2)^2(1024)^3  
