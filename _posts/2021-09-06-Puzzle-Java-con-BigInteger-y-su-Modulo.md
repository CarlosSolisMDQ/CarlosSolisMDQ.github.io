---
layout: post
author: Carlos
---


# java-puzzle

**puzzle encontrado en una web de ofertas de trabajo IT, me gustó y lo copié para resolverlo.**

*¡Desafío para desarrolladores!Si te interesa participar postulate a la búsqueda, para luego poder enviar la solución del siguiente puzzle.¿Podrías decirnos cuál es el resultado de ejecutar el siguiente código? (suponiendo que la máquina tiene los recursos suficientes para terminar de ejecutarlo). Por favor no olvides comentarnos cuál fue tu razonamiento para llegar al resultado.*  


{% highlight java %}

     

import java.math.BigInteger;

class Puzzle { 

    final static BigInteger M = new BigInteger("2021");

    private static BigInteger compute(long n) { String s = "";

    for (long i = 0; i < n; i++) { 
        s = s + n;
    } 

    return new BigInteger(s.toString()).mod(M); 
} 


public static void main(String args[]) { 
for (long n : new long[] { 1L, 2L, 5L, 10L, 20L, 67489454811002199L }) { 
    System.out.println("" + n + ": " + compute(n)); 
    } 
  }
}        

{% endhighlight %}

## **La solucion involucra aritmetica modular**

**Para acelerar la convergencia de la serie reducimos los operandos buscando sus modulos.**

### A(MOD) + b(MOD) = C(MOD)

*De esa manera reducimos el tamaño de los enteros que vamos a operar.*


{% highlight java %}       
import java.math.BigInteger;

public class puzzle {

        final static BigInteger M = new BigInteger("2021");

        private static String compute(long n) {
            String s = "";
            String a = new BigInteger(String.valueOf(n)).mod(M).toString(10);
            //System.out.println("a = " + a);
            for (long i = 0; i < Integer.parseInt(a); i++) {
                s = s + n;
                s = new BigInteger(s).mod(M).toString(10);
                //System.out.println("s = " + s);
            }

            return s;
        }

        public static void main(String args[]) {
            for (long n : new long[] { 1L, 2L, 5L, 10L, 20L, 67489454811002199L }) {
                System.out.println("" + n + ": " + compute(n));
            }
        }

}         
{% endhighlight %}