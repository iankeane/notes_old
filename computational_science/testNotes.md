Ian Keane  

---------------------  
Computational Science  
---------------------  


Tue Jan 12 09:24:10 EST 2016  
---------------------------------------------------------  

Notes at: cyn.help/CS/Scientific  


What is Scientific Computing  
    Taking the limited scope of the computer and emulating what a human  
        could do with infinite resources  
    Computers are limited in that they cannot understand concepts like  
        infinity  

Numbers  
    Rational - Q  
        def: n/m where n is in Z  
    Irrational  
        def: n/m where n is not in Z but n/m is in R  
    Integers - Z  
    Floating point  
    Count positive integers - Z+  
    Non-negative (natural) - N  
    Prime  
    Real - R  
        def: !!!  
    Complex - C  
    Even (includes zero)  
        def: x%0 = 0 or x = 2k when k is in Z  
    Odd  
        def: x = 2k+1 when k is in Z  
    Zero is non-positive and non-negative  
Intervals  
    Closed interval  
        ex: [1,10]  
        1,2,...,9,10  
    Open interval  
        ex: (1,10)  
        2,3,...,8,9  
    Interval brackets can also be mixed  

Functions takes an input and returns an output  
        ex: f(x) = x  
        takes x and returns x  
        typically f:R->R  
    Continuous functions  
        defined at every point in a domain  
        no discontinuities  
        unbounded or continuous in bounds  
    Computers cannot calculate continuous functions  
        cannot handle infinite bounds or infinite distance between  
            numbers  
        can only make approximations  
        ex: jpeg zooming causes pixelation  
Integers  
    Alphabet  
        digits: 0,1,...,8,9 
    Operators  
        + addition  
        * multiplication  
        ^ exponentiation  
    Defining 1024 in decimal  
        1024 = 1*10^3+0*10^2+2*10^1+4*10^0  
    Defining 1024 in binary  
        
Using 1 and 0  
    Can be thought of as a switch [on,off]  
        can also represent electrical current  
    Alphabet  
        digits: 0,1  
    Operators  
        0+0 = 0 | 0*0 = 0  
        0+1 = 1 | 0*1 = 0  
        1+1 = 0 | 1*0 = 0  
        1+1=0 | 1*1 = 1  
    

Thu Jan 14 09:30:00 EST 2016  
---------------------------------------------------------  

Numbers and Bases  
    All numbers can be broken down as above  
    The number being raised to the exponent is called the base  
        each additional digit represents another degree of freedom  
        base 10 digits: 1-9  
            ex: 101 = 1*10^2+0*10^1+1*10^0 = 101  
        base 2 digits: 0-1  
            ex: 101 = 1*2^2+0*2^1+1*2^0 = 5  
            these examples are called expansions 
        rewriting 1024(base 60) in base 10:  
            1*60^4+0*60^3+2*60^1+1*60^0  

Bit Architecture  
    An eight bit machine allows 8 bits in binary  
        i.e. the highest number is 11111111 = 255  
        this is 256 digits (counting zero)  
    During the cold war, the Russians tried to create trinary computers  
        using positive, negative, and zero  
        this was too fuzzy, caused the idea to fail  
    Hexadecimal can be understood quickly by computers and hold larger numbers  
        this is base 16  
        it can be easily translated into binary  
        uses digits 0,...,9 and a,...,f  
        255 can be represented in two digits as ff  
        thus hexadecimal can store all 8-bit numbers in two digits  
    How to convert hex to binary (easily)  
        ex: 59 in binary is 111011  
            1. make 8 digits  
                00111011  
            2. separate into groups of four  
                0011 1011  
            3. translate both to hex  
                3 b  
            4. concatenate  
                3b  
    We can store color in values of 255  
        this is what we mean by "8 bit color"  
        we can also write this in hex (ff)  
        we do not raise the base further, because it would not help  
        this is because the next base up is base 255, which is the same as 0-255  
            in base 10  
    Octal (base 8) can also be used to save some space  
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
    Base 4 does not contribute significant savings  


Tue Jan 19 09:52:46 EST 2016  
----------------------------  

Representing Decimals in Binary  
    In any expansion, the decimal can be representing by confinuing to 10^-1  
        ex: 1*10^1+1*10^0+1*10^-1+1*10^-2 = 11.11  
    !!! do binary  

Floating Points  
    Rational numbers with fixed maximum places  
        ex: 2/3 = .66(repeating) = .6667  
        error = abs(2/3 - .6667) = abs(2-3(.6667)) = .0001 = 10^-4  
    The precision is the number of significant digits we can store  
        ex: 1/64 can not be accurately stored at 10^-4 precision  
        error is 2.5*10^-5  

Floating Points and Scientific Notation  
    ex: 12.345 = 1.2345*10^1 = 12345*10^-3  
        12345 is the mantissa  
        mantissa begins and ends with a nonzero number  
        three parts to this, the mantissa, the base, and the exponent, and sign  
        these parts are stored in fixed bits  
    We can encode this number with the point at any place  
        this is why the data structure is called a "floating point"  
    The standard used for this is called IEEE 754  

Storing Floating Points  
    To store this in a 32-bit register (IEEE 754):  
        use one bit for sign (+ or -)  
        8 bits for the exponent  
        remaining bits for mantissa  
        no bits needed for base, because it is always base 2  
    # of bits allocated to the exponent tell us how big the number can be  
    # of bits allocated to the mantissa tell us the precision  
        by IEEE standard, 64-bit systems have 11 bits for exponent, 52 for  
            the mantissa  
    The exponent can go from 0-256, but has no sign  
        if we have no sign for the exponent, we can not store fractions  
        to solve this, half of the numbers 0-255 represent negative, half  
            positive numbers  
        0-127 = negative, 127-255 = positive  
            this is achieved by subtracting 127 from the exponent stored  
        exponent can go up to 128  
    To store the mantissa:  
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
    This denotes number of bits used to store a number  
        each memory register has 32 or 64 bits  
        on 32-bit, we can store 2^32 different numbers  
    Cpu has to be referenced at each byte  
        32-bit system can only keep up with 4-gigabytes at a time  

Exponential Math Note  
    2^10 = 1024  
    2^20 = 1024^2  
    2^32 = (2)^2(1024)^3  


Thu Jan 21 09:27:42 EST 2016  
----------------------------  

Floating Point Conversion (IEEE 754)  
    ex: -5.75  
    1. convert to binary  
        -101.111  
    2. shift decimal  
        -1.0111*2^2  
    3. hide first bit to make mantissa  
        -0111  
    4. translate the exponent  
        2+127 = 129 = 1000 0001  
    5. set first bit to the sign  
        1  
    6. make number  
        1 10000001 0111000... = sign, exponent, mantissa  
    7. pad with zeros to the right  
        1 10000001 01110000000000000000000  
    8. change format if desired  
        1100 0000 1011 1000 0000 0000 0000 0000  

Adding numbers in IEEE 754  
    Make the exponents the same, then do binary addition  
        ex: .01 + .1 (base 2)  
            =1*2^-2 + 1*2^-1 OR .01*2^1 + .1*2^1  
            if we can get it in the second form, we can just add them using  
                normal binary addition  
        .01 + .1 = .11  
    Converting to the same exponent is the hardest part  
        to do this in 754, change the exponent byte, then shift the mantissa  
        because of limited 64-bit storage, when we do this we may lose data  


Machine Constants  
    Largest number  
    Smallest positive number  
        negative sign, all zero exponent (-127), 22 zeros and a 1 in a mantissa  
            hidden bit may not be there ??? ask later  
            "if there is a register of all zeros, no hidden bit is present"  
    Smallest negative number  
    Machine epsilon  
        multiple definitions  
        distance between any two consecutive floating point numbers  
        the smallest number you can add without losing all data  
        the smallest distance between any two consecutive floating point number  
            in a machine, this is not infinite  
        2^-52  
            ??? ask later for notes in calculating this  
        epsilon size increases with architecture increases  
        the machine epsilon is larger than the smallest positive number  
            smallest "useful" number  

Vectors  
    A vector (in matlab) is an ordered, finite sequence of numbers  
        the number of slots in a vector is called the number of dimensions  
            ex: <1,2,3> has 3 dimensions  
            ??? so how do you talk about vectors of vectors?  
            2D vectors can be graphed on an x,y plane  
            3D vectors can be graphed on an x,y,z plane  
        each member of a vector is called a component  
    In a vector R, a plane is R X R  
        because of the shape of the plane, a vector can be graphically represented  
            as a line moving from origin in a direction  
        length of this line is the length of the vector  
        ??? so is a plane always square?  
        each vector also has a direction (represented graphically)  
    Canonically, the vector is always centered at the origin  
    2D example vector: V = <-1,2.5>  
        length is denoted ||V|| or |V|  
        ||V|| = sqrt(1+2.5^2)  
            if v = <x,y>, ||V|| = sqrt(x^2+y^2)  
    3D example vector: V = <1,2,3>  
        ???  
    Operating on vectors:  
        addition:  
            add coordinates: <0,1> + <1,0> = <1,1>  
        subtraction:  
            subtract coordinates: <1,1> - <0,1> = <1,0>  
    Equivalent vectors:  
        V is equivalent to W iff:  
            1. ||V|| = ||W||  
            2. V and W have the same direction  
        V and W are parallel if:  
            V and W have the same direction  


Tue Jan 26 09:29:39 EST 2016  
----------------------------  

Vector Geometry  
    Addition and subtraction  
        vectors can be added coordinate by coodrinate  
            ex: <a,b> + <x,y> = <a+x, b+y> 
                results in a longer vector  
        vector <a,b> is a line from the origin that points toward  
            ex: <a,b> - <x,y> = <a-x, b-y>  
                results in a shorter vector  
        to find the lengths, add or subtract the hypotenuses  
        what does proving they are equal (by definition of parallel) mean? ???  
        *note: the pythagorean theorem works in all dimensions  
    Dot product (inner product) (fig 2)  
        ex: <2,3,4> . <1,3,5>  
            take the sum of the products of the coordinates  
            2*1+3*3+4*5 = 31  
                takes two vectors and returns a number  
                dot and addition/subtraction are binary operators  
                    this means they take vectors of the same dimensions  
                <x1,...,xn> . <y1,...,yn> = SUM(i=1,n) xi*yi  
        law: V.W = V1W1 + V2W2 = ||V||||W||cos(theta) where theta is the angle  
            between V and W  
            ||V|| = sqrt(V1^2+V2^2)  
            ||W|| = sqrt(W1^2+W2^2)  
            (V.W)^2 = (v1^2+V2^2)(W1^2+w2^2)  
            ||V-W||^2=||V||+||W||-2||V||||W||cos(theta)  
            cos(theta) = algebraically reachable  
        if two vectors are parallel:  
            the difference between their vectors is 0  
            cos(0) = 1  
            so the dot product is the product of the lengths of the vectors  
        law: for any vector V, V.V = ||V||^2  
            so ||V|| = sqrt(V.V)  


Thu Jan 28 09:23:36 EST 2016  
----------------------------  

Dependence  
    ex: U and V are linearly dependent if:  
        there exists C1*U+C2*V = 0 for some C1,C2 != 0  
    ex: U and V are linearly independent if:  
        C1*U+C2*V = 0 -> C1 = C2 = 0  
    C1 and C2 can be found using substitution to determine dependence  
        we can test by setting the sum of the x's and y's to zero  

Matrices  
    A matrix can be thought of as an array of arrays  
        this means it can be an array of vectors  
        a matrix containing vectors instead of arrays does not change  
            operations on the matrix  


Tue Feb  2 09:31:29 EST 2016  
----------------------------  

Matrix Multiplication  
    Multiplication  
        number of rows must equal the number of columns  
            take the dot product of each row in matrix 1 and each column in  
                matrix 2  
        resulting array will be the smallest dimension of each matrix  
    Multiplication algorithm  
        matrix A = [a11,...,a1n],  
                       ...,  
                   [am1,...,amn]  
        matrix B = [b11,...,b1r],  
                        ...,  
                   [bs1,...,bsr]  
        for(:=1 to m){ // Select vector in A  
            for(:=1 to s){ // Select Vector in B  
                sum = 0;  
                for(k = 1 to n){ // Dot product  
                    sum += A[i][k]B[k][j];  
                }  
                C[i][j] = sum; // C is the output matrix  
            }  
        }  

        this yeilds m*r*n multiplications  
        
The Unit Vector  
    ex: V1 = <1,0,...,0>  
        V2 = <0,1,0,...,0>  
        U1 = <1,0>  
        U2 = <0,1>  
        ||U1||||U2||cos(theta) = U1.U2  
        ||U1|| = ||U2|| = U1U2  

Identity Matrices  
    ex: = [1 0]  
          [0 1]  
        constructed with unit vectors  
        multiplication by an ID matrix returns the same matrix  
    
Rotation Matrices  
    theta = angle between vector and rotated vector  
    alpha = angle between rotated vector and x axis  
    R(theta) = [cos(theta) -sin(theta)]  
               [sin(theta)  cos(theta)]  
        [x2] = [cos -sin] [x1] =  [x1cos - y1sin]  
        [y2]   [sin  cos] [y1]    [x1sin + y1cos]  


        [x1 y1] * [cos -sin] =  [cos-  -sin-][x1]  
                  [sin  cos]    [sin-  cos- ][y1]  
        !!! wrong?  

        cos(theta) = sin(-theta)  

Transposition Matrices  
    Notation is A^T for transposition matrix  
    Transposition is multiplication by the same matrix flipped vertically  
    ex:     [a1 a2]         [a1 a3 a5]  
        A = [a3 a4]  A^T =  [a2 a4 a6] 
            [a5 a6]  
    !!! what is it used for?  
        can be useful for rotation  
            multiplication of V by a rotation matrix rotates left  
            multiplication of V^T by a rotation matrix rotates left  


Thu Feb  4 09:24:38 EST 2016  
----------------------------  

More Rotation  
    A vector can be rotated left by dotting by the rotation matrix  
        can be rotated right by transposing and dotting by the rotation matrix  
        !!! is all matrix multiplication a dot product at this point?  
    Two matrices can be rotated by the same amount by multiplying by the  
        rotation matrix  
        ex:   [Vx Wx][cos -sin]  
              [Vy Wy][sin  cos]  

Rotation in Higher Dimensions  
    Requires a bigger matix (more axes)  
        Rotation around z:  
            [x][cos  -sin    0 ]  
            [y][sin   cos    0 ]  
            [z][ 0     0     1 ] 
        Rotation around y:  
            [x][cos    0   -sin]  
            [y][ 0     1     0 ]  
            [z][sin    0    cos] 
        Rotation around x:  
            [x][ 1     0     0 ]  
            [y][ 0    cos  -sin]  
            [z][ 0    sin   cos]  
            !!! wrong?  
    Complex rotations can be done by combining these  


look into asymptote vector graphics language  


Tue Feb  9 09:55:51 EST 2016  
----------------------------  

Linear Algebra  
    2x + y = 1  
    x + 3y = 2  

Look into:  
    Gaussian Elimination  
