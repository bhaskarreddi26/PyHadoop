- val is not reassignable.
- var is reassiganable (rarley used)
- lazy val is lazyly update value example 

           lazy val a={println("evaluated");5}
           evaluated
           a: Int = <lazy>
           
           a
           a: Int = <lazy>
           res1: Int = 5

- lazy val will not evaluated until referenced 
- Any subsequent call to the val will return the same value when initially called upon
- There is no such initially called upon 
- lazy val can  be forgivingif an excetion happends 


Valid OPCHAR : Unicode Character from \u0020-\u007F

http://unicode.org/charats/PDF/U000.pdf