---
layout: post
title: "F# Mentorship Program : Week-2"
subtitle: " \"F# Software Foundation’s Mentorship Program. Week-2\""
date: 2017-10-29 20:41:49
author: "Nithin VR"
header-img: "FSharpInViolate.png"
catalog: true
tags:
    - F#
---

Summary:
I updated my progress in both sharp for fun and profit and hacker rank, we discussed one of my solution in hacker rank. 
Oleg suggested to try Fibonacci in different ways

My Initial Code
```CSharp
//Enter your code here. Read input from STDIN. Print output to STDOUT
let distance (x1:int,y1:int) (x2:int,y2:int) =
    let xDiff = abs x1-x2
    let yDiff = abs y1-y2
    let sqrSum = (pown xDiff 2)+( pown yDiff 2)
    sqrt (double sqrSum)
    
let getPoint (s:string) =
    let va = 
        s.Split(' ') 
        |> Array.map System.Int32.Parse
    (va.[0], va.[1])


[<EntryPoint>]
let main argv = 
    let t = System.Console.ReadLine()|> int
    let values = 
        Seq.initInfinite(fun _ -> System.Console.ReadLine())
        |> Seq.takeWhile(isNull >> not)
        |> Seq.map getPoint
        |> Seq.toList

    let first, rest  = values.[0], List.tail values
    
    let foldFunc (perimeter, prevPoint) nxtPoint =
        perimeter+(distance prevPoint nxtPoint), nxtPoint

    let (finalPerimeter , last) = List.fold foldFunc (0.0, first) rest
    
    printfn "%f" (finalPerimeter + (distance first last))
    0
```
Cleaned Up Code
```CSharp
//Enter your code here. Read input from STDIN. Print output to STDOUT
let distance ((x1:int,y1:int), (x2:int,y2:int)) =
    let xDiff = abs x1-x2
    let yDiff = abs y1-y2
    let sqrSum = (pown xDiff 2)+( pown yDiff 2)
    sqrt (double sqrSum)

let getPoint (s:string) =
    let [| x; y |] = 
        s.Split(' ') 
        |> Array.map System.Int32.Parse
    x,y

[<EntryPoint>]
let main argv = 
    let t = System.Console.ReadLine()|> int
    let mutable firstPoint = (0,0)
    let values = 
        Seq.init t (fun i -> let currentPoint = System.Console.ReadLine() 
                             currentPoint)
        |> Seq.map getPoint
        |> Seq.toList
        
    let lines = Seq.pairwise (values.[0]::(List.rev values))
    
    let perimeter = 
        lines
        |> Seq.map distance 
        |> Seq.sum
    
    printfn "%f" perimeter
    0
```

New concepts:
- yield , !yield
- seq init, Seq.pairwise 
- let lines = seq { yield values.[0]; yield! values |> Array.rev;  }
- Tail call

### Here are the few questions we discussed
1. Is None is same as null of C#?
Yes. When you convert the F# to C# it will be null. Option monarch must have some , none or some

2. Is there any types for None or Some?

3. Is List.fold is recursive calling or for loop inside implementation?

4. Is Seq.unfold similar to lazy list in C#? Is it storing any state internally?
Internal structure iterator and we a calculating.

5. I was experimenting with the partial application, is the parameter passing always follow from the left to right? (I verified with one example)
    Yeah.[23/09/17, 10:41:31 AM] Oleg Golovin: let fn a b c = ()
    let fn1 = fn a
    fn1 b c
    fn1 (b c)
    let fn2 a: int -> int = fun b -> 0
    int -> int -> unit
    let fn a b c = ()
    fn1 (fn2 a)

6. While finding the type by type inference do we actually handle the runtime case? 
For example : 
    `let x = 2147483647 + 1` No error 
    `let y = 2147483648 ` Shows error FS1147: This number is outside the allowable range for 32-bit signed integers