---
layout: post
title: Linear Algebra Done Right
---
Personal Notes from Linear Algebra Done Right by Sheldon Axler

---


The special thing about linearity is homogeneity i.e if I can prove something in one region of space then it must be true in all regions. This is as try for numeric relationships as 
it is for theorems. Linearity is a kind of homogeneity in the sense that things like vectors, distances, rates of change and transforms behave very predictably throughout the space.

Rules defining a vector space:

Pvectoraxioms.png


> A subset U of V is called a subspace of V if U is also a vector space (using the same addition and scalar multiplication as > on V ).


**Conditions of a Subspace**

> If U is a subset of V,then to check that U is a subspace of V we need only check that U satisfies the following:
> - additive identity
> $0∈U$
> - closed under addition
> $u, v ∈ U$ implies $u + v ∈ U$ ; 
> - closed under scalar multiplication
> $a∈F$ and $u∈U$ implies au∈U  

**Joining spaces - Direct Sum**

The union of two subspaces is not always a vector space. 

E.g) If x-axis and y-axis are thhe subspaces then their union includes both (3,0) and (0,5), whose sum, (3,5), is not in the union.

The next logical question would be *"How do I then define the joining of two spaces?"* 
The answer lies in the direct sum. The idea is to fill the caused by the addition operation. Put elements which stop the union of spaces to be a space by putting elements required into the collection by considering additions over the spaces as well.  

Pdirectsum

A direct sum does consider additions of the space to belong to their direct sum, unlike the example above. A vector field can be thus decomposed into a number of direct sum elements and each element can be looked at under closer observation. 

Direct sum implies that the only way to write 0 is by taking all $u_i's$ to equal 0. The intersections of all the 
spaces $U_i's$ is the null set. Refer to the proof of these in the book. A basis spanning a space can be thought of a direct sum. Additions are required and every point is uniquely reached. 

The two properties of direct sums are *V=U+W and U intersection W ={0}*




## **Ch2 Finite Dimensional Vector Spaces - Basis , Span and Dimension**

> A linear combination of a list $v_1....v_m$ of vectors in V is a vector of
> the form
> $a_1v_1 +....+ a_mv_m$
> where $a_1.....a_m$ belong $F$.
> The set of all linear combinations of a set of vectors is called its span.

**Linear independace** is defined 

PLinearIndep

We see that any point being a unique sum is equivalent to saying 0 is a unique sum. The only way to reach a point should be through a unique combinations of vectors.
PLinearIntri

In the image there are two ways to the tip of R. Go directly through R or A+B. This implies I can get to 0 by staying at 0 or going A+B-R.
Thus if I can get to 0 in more than one way, I can get a midpoint in the path in more than one way. A unique point representation implies the only solution to $\sum a_iv_i = 0$ is $\forall i, a_i=0$.
This condition is called linear independance. Linear independace maens that as no vector can be written as a sum of the others it provides a new component that the others need to get
to some point. If they above condition is not true, it means that the vectors can add in a distructive manner, but this wont be the case each vector has unique a component others can't get to.

> A basis of V is a list of vectors in V that is linearly independent and spans V. 

> Every spanning list can be reduced to a basis by removing linearly dependant vectors iteratively. Likewise, any linearly indepant list of vectors can be extended to a basis of the vector space by addition of linearly independant vectors. 

These two notions are used in many proofs. 

> 2.13 says that if U is a subspace of V, then U can be extended to V through a direct some with some W. Here we use the fact that other linearly independant vectors can be added to U to form a spanning set of V.

A key point is that if I have a set of linearly independent vectors equal to the dimension of the space then it must be a basis. This works the other way as well:
> Suppose V is finite-dimensional. Then every linearly independent list of vectors in V with length dim V is a basis of V.

**Dimension**

A reasonable definition should force the dimension of $F^n$ to equal $n$. Homewever, finite-dimensional vector space in general have many different bases
This definition makes sense only if all bases in a given vector space have the same length. Fortunately that turns out to be the case.

> 2.14 Theorem: Any two bases of a finite-dimensional vector space have the same length.

My Proof: Let U and W be two different sized bases of V. Pick the one containing the smaller number of elements, say $n$. As U is a spanning list any vector is W can be expressed as a linear combinations of U's.
Express the first $n$ vectors in W as a combintion of U's. This is necessarily a spanning list as it is equal to U. Thus W cannot be longer than U. 

From this an important Proposition arises: 
> 2.16) If V is finite dimensional, then every spanning list of vectors in V with length dimV is a basis of V

> 2.17) If V is finite dimensional, then every linearly independent list of vectors in V with length dim V is a basis of V .

> 2.18) Dimension of a Sum: 
> If U1 and U2 are subspaces of a finite-dimensional vector space, then
> dim(U1 +U2)=dimU1 +dimU2 −dim(U1 ∩U2).
This formula for the dimension of the sum of two subspaces is analogous to a familiar counting formulae.

Try proving the following:
dimDirectSum.png

Suppose V is finite dimensional. If $U_1 , . . . , U_m$ are subspaces of V such that $V = U_1 ⊕ · · · ⊕ U_m$, then
$dimV =dimU_1 +···+dimU_m$

These one dimensional subspaces can be constructed from any basis. If $v_i.....v_n$ is a basis then each $v_i$ is a subspace of dimension 1. The intersection of any of these subspaces only includes the origin or 0 vector.


This exercise deepens the analogy between direct sums of sub- spaces and disjoint unions of subsets. Specifically, 
compare this exercise to the following obvious statement: if a finite set is writ- ten as a disjoint union of subsets, 
then the number of elements in the set equals the sum of the number of elements in the disjoint subsets.
The difference from sets is that our spaces are closed under addition and multiplication operations. 


## **Ch3 Linear Maps**

PLinearmapdefn

$L(V,W)$ is used to denote a linear map from $V$ to $W$. Linear maps eximply the homogenoity offered by linear algebra. These two statements mean that a transform acts on individual units of vectors. There is no scaling or
compounding effect that takes place when vectors change or become large. Things are very predicatable. If T(10)=5 then T(20)=T(10)+T(10)=10.
Transforms work with proportions. A function $T(x)=2x+2$ does not obey our linearity cause $+2$ has nothing to do with $x$. If two points $a$ and $b$ have distance $a-b$ then after
a transform they will be $T(a-b)$ away. So the space between two points is stretched only according to the difference vector and not the absolute values of the points. Likewise the vector $a-b$ between any two points is stretched exactly the same
way as this one.

Comments on composition ST

Null space
> For T ∈ L(V,W), the null space of T, denoted nullT, is the subset of V consisting of those vectors that T maps to 0:
> nullT ={v ∈V :Tv =0}.
> If T ∈ L(V,W), then nullT is a subspace of V.

A linear map T: V → W is called injective if whenever u,v ∈ V and Tu = Tv, we have u = v.
> 3.2 Proposition: Let T ∈ L(V , W ). Then T is injective if and only if null T = {0}.

Injective is one-one. Let a and b be some points in space. If T(a) = T(b) then T(a-b)=0. This means the line between a and b is squased to 0.
Pabsub
Thus all vectors a-b go to 0. So we colapse one dimension by placing this vector at every point in space. However if a-b=0 then T must be injective.

**Range of a Transform**

> For T ∈ L(V,W), the range of T, denoted rangeT, is the subset of
> W consisting of those vectors that are of the form Tv for some v ∈ V :
> rangeT ={Tv :v ∈V}.

RangeT is the output space of T.

Both the range space and the null space form a subspace.
> A linear map T : V → W is called surjective if its range equals W . The output space is spanned by Tv.


**Rank-Nullity Theorem**

> 3.4 Rank-Nullity Theorem: If $V$ is finite dimensional and $T ∈ L(V,W)$, then range $T$ is a finite-dimensional subspace of $W$ and
$dimV =dimnullT +dimrangeT$.


A simple extension of the above ideas leads to the rank-nullity theorem. Let $dimV = n$. Let $dim nullT = k$. Let B be some basis s.t the nullspace are elements of the basis. Excluding the null space we have $n-k$ independant vectors left in $V$. Each is a one-dimensional subspace which is mapped by $T$
to another one-dimensional subspaces. So the output dimensional space is now $n-k$
Thus all vectors in the basis either are part of the null space or mapped to one-dimensional output spaces.
Hence $dimV = dimnullT +dimrangeT$

Now we come to some interesting cases of the above theorem. 

> 3.5 Let $T ∈ L(V,W)$. If $V$ and $W$ are finite-dimensional vector spaces such that $dim V > dim W $, then no linear map from $V$ to$ W$ is injective.

Proof: 

$dimV =dimnullT +dimrangeT$

$dimnullT=dimV-dimrangeT$
       
as $dimV>dimrangeT$
       
$dimnullT>0$
       
Thus by 3.2, the map is not injective.


If $V$ is being pushed to a span a smaller space and a one-dimensional subspace can only map to another one-dimensional subspace, some of its subspaces must be taken to 0.
       
> 3.6 Let $T ∈ L(V,W)$. If $V$ and $W$ are finite-dimensional vector spaces such that $dim V < dim W$ , then no linear map from $V$ to $W$ is surjective.

Proof: $dimrangeT =dimV − dimnullT ≤ dim V < dim W $
Since one-dimensional subspace can only map to another one-dimensional subspace. We don't have enought subspaces in $V$ to map W.

3.5 and 3.6 can be applied to know if systems of linear equations have solutions or not. 
Phomoeq1
Phomoeq2

In this case if $n>k$ i.e more variables than equations then we are projecting from a bigger to smaller space. If this transform spans the space then we would have a solution but it may not.
If$ k>n$, then we may have a solution if $c_1.......c_n$ belong to rangeT but the transform does not span the possible range space so there may not be one.

## **Linear Maps as Matrices**

Matrices are representations of linear maps in rectangular array form. A matrix $M T,(v_1,...,v_n),(w_1,...,w_m) $ takes elements in the basis $v_1.......v_n$ to a output space with basis $w_1.....w_m$.
Matrices obey the linear notions vector addition and scalar multiplication and are a vector space themselves.
A composition of two linear maps is easy to find out. Matrix Multiplcation is defined the way it is so compositions of matrices, which are really compositions of linear transforms, behave as they should.

**Invertibility**

> 3.17 Proposition: A linear map is invertible if and only if it is injective and surjective.

Two vector spaces are called **isomorphic** if there is an invertible linear map from one vector space onto the other one. As abstract vector spaces, two isomorphic spaces have the 
same properties. From this viewpoint, you can think of an invertible linear map as a relabeling of the elements of a vector space.

Isomorphism exists between two same dimensional spaces and allows us to reason about one through the other. A basis transformation is an isomorphism as it is
just a relabeling of the same space with different basis vectors. Thus if we know how these bases vectors corrospond, then knowing something about one allows us insight into the other due to the corrospondece being homogenous across the entire space.
Linear maps from $V$ to $V$ are called operators and have some useful properties.

> 3.21 Theorem: Suppose V is finite dimensional. If T ∈ L(V,V), then the following are equivalent:
> - T is invertible
> - T is injective
> - T is surjective


Operators also have the propoerty that if $v_1....v_n$ is a basis and T is any of the above then $T(v_1)....T(v_n)$ is linearly independant.
Proof
$a_1v_1....a_nv_n=0$ only for $a_1=a_2=...=a_n=0$
if $T(b_1v_1)+....+T(b_nv_n)=0$
then $T(b_1v_1......b_nv_n)=0$
but as T is surjective this means it is injective and as it is true for  $b_1=b_2=...=b_n=0$, it can only be true for this case.

 
## **Ch 5 Eigenvalues and Eigenvectors**

**Invariant subspaces**

> Suppose $T \in \mathcal{L}(V)$ A subspace U of V is called invariant under T if $u \in U$ implies $Tu \in U$

If the dimension of $U$ is 1, then $T$ just scales $u$ but if dim>1 then $Tu$ could lie anywhere on the plane spanned by members of $U$
Obviously ${0}$ and $V$ are invariant under an operator. So are $nullT$ and $rangeT$. $0$ is always in a set. Therefore
If $u \in nullT$, then $Tu = 0$, and hence $Tu \in nullT$. Thus nullT is
invariant under T.
If $u \in range T$, then $Tu \in range T$ as $Tu$ always outputs a member of the range(including 0 is a key point). Thus $range T$ is invariant under T.

> One dimensional invariant spaces are called eigenvectors and are of the form:
> $T u = λu$

The equation $Tu = λu$ is equivalent to $(T −λI)u = 0$, so $λ$ is an eigenvalue of $T$ if and only if 
$T − λI$ is not injective. By 3.21, $λ$ is an eigenvalue of $T $if and only if $T − λI$ is not invertible, and this happens if and 
only if $T − λI$ is not surjective.

The next theorem states eigenvectors must be linearly indepdant.
PeigenLI

This is easy to see as if they were linerly dependant then I could write one in terms of the other. Now when I apply $T$, the vector would be
scaled according to other eigenvalues and vectors and not its own. This naturally leads to the theorem that an operator has at max $dimV$ eigenvectors.

Eigenvalue existence proof:

The main reason that a richer theory exists for operators (which map a vector space into itself) than for linear maps is that operators can be raised to powers. 
We shall define that notion and the key concept of applying a polynomial to an operator. 

We can define a morphism $S$ from the space of polynomials on reals to the space of polynomials of operators as
$S: p(z) -> p(T)$
Now we show that $S$ must obey certain propoerties in both directions. This will allow us to do to polynomials of operators what we do to real poynomials.

Defination:
Suppose $T \in \mathcal{L}(V)$ and $p \in \mathcal{P}(\mathbf{F})$ is a polynomial given by
$p(z)=a_{0}+a_{1} z+a_{2} z^{2}+\cdots+a_{m} z^{m}$ for $z \in \mathbf{F}$. Then $p(T)$ is the operator defined by
$p(T)=a_{0} I+a_{1} T+a_{2} T^{2}+\cdots+a_{m} T^{m}$

Properties:
Proof that polynomial to linear operators are linear: http://mathonline.wikidot.com/polynomials-applied-to-linear-operators

Ppolyoper

Proving that $(pq)(T)=p(T)q(T)$ is a critial part of the morphism. This is what allows us to factorize a polynomial of operators.
The prove first describes $(pq)(z)$ on the reals. Clearly it is a valid expansion. Then after applying our operator $S$, we take the exact
expression to the space of polynomials as $(pq)(T)$.(Keep in mind the summations is such that set j then sum over all k then set j and so on). This can then be simplied as shown to get 
the wanted $p(T)q(T)$.
Ppolyeg

Peigenproof

$v$ is not necessarily the eigenvalue. $v$ is transformed multiple times and one of the $(T= \lambda_i I)$ sends it to 0. $v$ is chosen as any random vector and the above is true for all $v \in V$. We can think of the
terms before the non-injective one as killing components of $v$ that are not in the eigendirection.


Upper Triangular Matrix

A matrix is called upper triangular if all the entries below the di- agonal equal 0.
PUTthm
The special thing about UT matrices is that there are invariant subspaces that can easily be seen from the matrix representations.
Supposed I am in 6D. The second proposition says that if I take $v_3$ then $Tv_3$ belongs in the 3D cube spanned by the basis vectors. We have chosen the basis such 
that these are the $x,y,z$ axis in our space. The spaces are invariant i.e any vector belonging to the $x,y$ plane will stay on the plane and similary for any other dimension.
Think of it as iteratively adding a dimensional for each $v_k$.

LookUp
Cases of degenrate, multiple eigenvalue, no eigenvalues, arithmic and geometric multiplicity


LookUp
When does this fail in reals? 


UT proof for complex spaces:
P Utproof1 and 2

The sketch of this proof is as follows:
Show it is true for dim = 1 
Now using the fact that every complex vector space has atleast one eigenvalue, we consider the range space without that direction.
Any vector that belongs to $range(T - \lambda I)$ clearly cannot be the eigenvalue and cannot map to an component of the eigenvalue(T is an operator from $V$ to $V$).
Thus this subset is invariant under T as claimed above.
Now we consider an smaller operator only over this subspace. A way to think about this is that make a basis of $dimV$ with the eigenvector being the last dimension. Now thrown away that last dimension
and I have a smaller vector space like (x,y,z....g,0)->(x,y,z....g)
Now using our induction hypothsis there is a UT matrix on this space.
We choose this as our basis and extend it back to $dimV$ using the eigenvector found earlier(the proof accounts for eigenvectors with same eigenvalues hence then $v_1...v_n$ addition)
Our smaller space is invariant due to induction and added vectors are also due to being eigenvectors.
Thus because we 5.12b) that every $Tv_k$ is is contained in the previos spans there must exist an UT matrix. 


This does not hold on real spaces

If T has an upper-triangular matrix with respect to some basis of V. Then the eigenvalues of T are the entries on the diagonal of that upper-triangular matrix.
T is invertible if and only if all the entries on the diagonal of that upper-triangular matrix are nonzero. Easy to see, as if one were 0, it could be written as a linear 
combination of the ones before it and thus nullT>0.

If T has dimV distinct eigenvalue then the eigenbasis can be used to form a diagnoal basis for T.

The next theorem says something very interesting about the way rotation of planes work. It says if I am rotating space, then there must be some 2D plane that I am holding and rotating.
5.24 Theorem: Every operator on a finite-dimensional, nonzero, real vector space has an invariant subspace of dimension 1 or 2.
