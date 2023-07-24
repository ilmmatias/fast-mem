# Optimized memory functions for AMD64

This is an implementation of fast memset and memcpy functions based on the research from Microsoft's [Building Faster AMD64 Memset Routines](https://msrc.microsoft.com/blog/2021/01/building-faster-amd64-memset-routines).  
Just like Microsoft's kernel mode implementation, we also use only SSE2 (instead of AVX2).  
The performance of both implementations would be the same, except that we're not using REP STOSB yet, so we lose a bit of performance when going over 800 bytes.

The memcpy implementation has been derived from memset (instead of broadcasting the same byte across all registers, we just read the source).  
I didn't benchmark it too much, but it seems to be fast enough for me usecase (kernel-mode memcpy, for my usual hobby OS projects).

The strlen implementation is my attempt at using SSE2 instead of just a dummy implementation, it is considerably slower than glibc's implementation, so there's still a lot of room for improvement.

Pull requests and issues (bug reports and feature requests) are welcome!
