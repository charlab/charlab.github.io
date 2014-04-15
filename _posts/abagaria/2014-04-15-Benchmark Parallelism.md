RAY
----

Number of threads in each block = 16 x 8 = 128 threads

Number of thread blocks = (64/16, 64/8) = (4,8) 

Thus, number of thread blocks in a queue at any given time = 4 x 8 = 32.

Coulombic Potential (CP)
-------------------------

Number of threads in each block = 16 x 8 = 128 threads.

VOLSIZE_X = 512         VOLSIZE_Y = 512

BLOCKSIZE_X = 16        BLOCKSIZE_Y = 8

UNROLLX = 1

Grid Size in the x dimension = Gsz.x = 512/16 = 32

Grid Size in the y dimension = Gsz.y = 512/8 = 64

Grid Size in the z dimension = UNROLLX = 1

Thus the number of thread blocks issued  = (32, 64)

and the number of blocks in the queue at a given point in time = 32 x 64 = 2048 thread blocks.
