#uni 
PyTorch is an open-source machine learning library developed by Facebook's AI Research lab (FAIR).
# Tensors
```python
import torch

x = torch.tensor([1,2,2,2,3,4])
.zeros(3,4)
.rand
.randn

# moving tensor to GPU
if torch.cuda.is_available():
	x_gpu = x.to('cuda')
	# oppure
	x_gpu = x.cuda()
```
# Autograd
```python
x = torch.tensor([2,0], requires_grad=True)
y = //
z = x**2 + y**3

z.backward() # compute gradients

print(x.grad)
print(y.grad)
```
- `requires_grad=True` enables gradient tracking
- `backward()` computes gradients with respect to all tensors with requires_grad=True
# DataLoaders
Data structures that launch a new thread, specialized for loading data and being able to run CPU and GPU in parallel.