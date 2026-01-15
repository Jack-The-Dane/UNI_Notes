Assume that:
$$u(x,y) = f(x) \cdot g(y)$$
PDE (First Order):
$${\partial u \over \partial y} = y {\partial u \over \partial x}$$
Substitute u into equation:
$$f(x)\cdot g'(y) = y\cdot f'(x)g(y)$$
separate variables:
$${g'(y) \over yg(y)}= {f'(x)\over f(x)} = Constant = C$$
$$f'(x) \cdot {1 \over f} = C$$
$$\int{1\over f} df = \int C dx$$
$$\ln(f) = cx+d$$
$$f=e^{cx+d}$$
$$f = Ae^{cx}$$
Do the same for the g function, remember to multiply y over to C:
$$g=B\cdot e^{c y^2 \over 2}$$
so:
$$u(x,y) = D\cdot e^{c(x+y^2)\over 2}$$

Finding a specific solution using boundary conditions:
$$u(1,1) = e \rightarrow D = 1$$
$$u(1,1) = e^{c(1+{1\over 2})} \rightarrow c= {2\over 3}$$
$$u=e^{{2\over 3}(x+{y^2 \over 2})}$$

## Example First order PDE
$$xy{\partial u \over \partial x}= yu + {\partial u \over \partial y}$$
$$xyf'g = yfg + fg'$$
$${xf' \over f} = 1 + {g' \over yg} = C$$
$${df \over dx} = {C \over x} $$
Integrate to find funtion of x

$${dg \over dy} {1 \over g}{1\over y} = C-1$$
Integrate to find function of y.
Multiply the 2 together at the end.
Video: Separable solutions to PDEs, Tom Rocks Math

