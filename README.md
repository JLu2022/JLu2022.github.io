<head>
  <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
  <script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
</head>
theme: minima

![[Pasted image 20221201111543.png]]
All materials are modified from https://www.youtube.com/watch?v=hQ4UNu1P2kw

We are going to see a intuitive way to Lagrangian Multiplier. 

If we have a curve, $$f(x,y)=x^{2}e^{y}y=C\ ,s.t.\ g(x,y)=x^{2}+y^{2}=4\tag{1}$$ where C is a constant. We would like to find the maximum C or the value of $$f(x,y)$$ while keeping the constraint that $$(x,y)$$ need to stay on $$g(x,y)$$.

One intuitive inference of the maximum value of C occurs when $$f(x,y)$$ tangent with $$g(x,y)$$. ![[Pasted image 20221201112230.png]]
On the tangent point, the gradient of $$f(x,y)$$ and $$g(x,y)$$ should be parrell with each other. This is mathematically noted as $$\nabla f(x,y)=\lambda \nabla g(x,y)\tag{2}$$ 
We can construct a function $$\mathcal{L}(x,y,\lambda)=f(x,y)-\lambda( g(x,y)-b) \tag{3} $$ , where b is actually the constant 4 in equation 1 we note it as a arbitrary constant $$b$$ .

By setting the gradient of $$\mathcal{L}$$ as 0 $$\Rightarrow$$ 
$$ \nabla\mathcal{L}=\left\{
\begin{aligned}
\frac{\partial \mathcal{L}}{\partial x} \\
\frac{\partial \mathcal{L}}{\partial y} \\
\frac{\partial \mathcal{L}}{\partial \lambda}
\end{aligned}
\right\}=\left\{\begin{aligned}0\\0\\0\end{aligned}\right\}
\tag{4}
$$
This is the packaged equation 2: $$\nabla\mathcal{L}(x,y,\lambda)=\mathbf{0}\Leftrightarrow\nabla f(x,y)=\lambda\nabla g(x,y) \tag{5}$$  Because:
$$\frac{\partial \mathcal{L}}{\partial x}=\frac{\partial f}{\partial x}-\lambda\frac{\partial g}{\partial x}=0 \tag{6}$$
$$\frac{\partial \mathcal{L}}{\partial y}=\frac{\partial f}{\partial y}-\lambda\frac{\partial g}{\partial y}=0 \tag{7}$$ $$\frac{\partial \mathcal{L}}{\partial \lambda}=-g(x,y)+b=0 \tag{8}$$   Equation (6) and (7) are equivalent to equation 2, while equation (8) is the constraint function $g(x,y)=b$

It seems that the Lagrangian is just to package a function and its constraint and makes no magical difference. However, this is important for using computer to solve the optimal value problem. Because comparing to solving the optimal value problem of a function with constraint, it is always easy for a computer to solve another function which is equivalent but unconstrained. 

If the a set of tuples $$(x^{*},y^{*},\lambda^{*})$$ satisfies $$\nabla \mathcal{L} =0 \Leftrightarrow f_{max}=f(x^{*},y^{*})$$ , it is obvious that the value of $$x^{*}\ or\ y^{*}\ or\ \lambda^{*}$$  are related to the value of constant $$b$$ in 
$$f(x,y)=x^{2}e^{y}y=C\ ,s.t.\ g(x,y)=x^{2}+y^{2}=b\tag{1}$$
Because if the constraint change the maximum/optimal value and the tangent point changes. 
This makes $$f_{max}$$ to be a function of the value of $b$ as well, if we would like to change $b$ and observe how the maximum value of $$f$$ is going to change on that way.
We hence can construct:
$$f_{max}(b)=f(x^{*}(b),y^{*}(b))$$ A important lemma:
$$\lambda^{*}=\frac{df_{max}(b)}{d(b)}$$ The lemma means that $$\lambda^{*}$$ is the changing rate of $$f_{max}$$ with $$b$$.
$$Proof:$$ 
$$Plug\ (x^{*},y^{*},\lambda^{*})\ to\ \mathcal{L}(x,y,\lambda)=f(x,y)-\lambda( g(x,y)-b)$$ 
$$\Rightarrow \mathcal{L}(x^{*},y^{*},\lambda^{*})=f(x^{*},y^{*})-\lambda^{*}(g(x^{*},y^{*})-b)$$ 
$$\because g(x,y)=b$$ 
$$\therefore g(x^{*},y^{*})-b=0\ \Rightarrow \mathcal{L}(x^{*},y^{*},\lambda^{*})=f(x^{*},y^{*})=f_{max}$$
$$\because x^{*},\ y^{*}\ and\ \lambda^{*}\rightarrow b$$ 
$$\Rightarrow \mathcal{L}(x^{*}(b),y^{*}(b),\lambda^{*}(b))=f(x^{*}(b),y^{*}(b))-\lambda^{*}(b)(g(x^{*}(b),y^{*}(b))-b)$$ 
By using chain rule
$$\Rightarrow \frac{d\mathcal{L}}{db}=\frac{\partial\mathcal{L}}{\partial{x^{*}(b)}}\cdot\frac{dx^{*}(b)}{db}+\frac{\partial\mathcal{L}}{\partial{y^{*}(b)}}\cdot\frac{dy^{*}(b)}{db}+\frac{\partial\mathcal{L}}{\partial{\lambda^{*}(b)}}\cdot\frac{d\lambda^{*}(b)}{db}+\frac{\partial\mathcal{L}}{\partial{b}}\cdot\frac{db}{db}$$ 
$$\because \nabla \mathcal{L}=0$$
$$\therefore \frac{\partial\mathcal{L}}{\partial{x^{*}(b)}}=0, \frac{\partial\mathcal{L}}{\partial{y^{*}(b)}}=0, \frac{\partial\mathcal{L}}{\partial{\lambda^{*}(b)}}=0$$ 
$$\Rightarrow \frac{d\mathcal{L}}{db}= \frac{\partial\mathcal{L}}{\partial{b}}$$ 
Write the function $$\mathcal{L}$ on the tuple $(x^{*},y^{*},\lambda^{*})$ as $\mathcal{L}^{*}$$
Writing $$\mathcal{L}=\mathcal{L}(x,y,\lambda,b)$$ 
$$\Rightarrow \frac{\partial\mathcal{L}}{\partial{b}}=\lambda=\frac{d{\mathcal{L}^{*}}}{db}$$  
$$\because f_{max}(b)=f(x^{*}(b),y^{*}(b))=\mathcal{L}(x^{*},y^{*},\lambda^{*})$$ 
$$\therefore \lambda^{*}=\frac{df_{max}(b)}{d(b)}$$ 

[Link to Another Repository](https://github.com/JLu2022/JLu2022.github.io/blob/ace8309f16ab3f9ba79c9958f2814be5f503df63/oo/oo.md)
