# pca_face_recognition
Pca face recognition with c++ coding;Changzhou University  junior spring semester AI class experiment.
# (0)Math Theory of PCA Algorithm
- Problem to solve:
  We have a set of datas(with the same dimension) to describe a kind of feature，but many features of these datas are kind of redundant.Try to find a way to readuce the dimension of the datas and keep the most obviously features.
- Solve:

Assump we have a set of datas:
<img src="https://render.githubusercontent.com/render/math?math=D_{dxn}">
(the dimension of data is d,the number of datas is n,d and n may be very huge)

# (1)Experiment Environment
- Win10 X64
- CodeBlocks
- opencv(just few steps to config CodeBlocks with opencv,following [Link](https://blog.csdn.net/libizhide/article/details/108417216?spm=1001.2014.3001.5501))
# (2)Outline
- Review the math theory of PCA algorithm
- Try to understand the procedure of PCA face recognition
- Do basic coding to know about the PCA face recognition
- Basic PCA recognition (verification of algorithm)
- Precision benchmarking
- Precision boosting
- Application
- Summary
# (3)Main Codes Structure
## Traing
- Read training images 
- Transform training image matrixs to row vectors data DS
<img src="https://render.githubusercontent.com/render/math?math=Ds_{dxn}">
- perform PCA function to get "MEAN", "EIGENVECTORS" and "EIGENVALUES"


```cpp

/**
The class is used to calculate a special basis for a set of vectors. The
basis will consist of eigenvectors of the covariance matrix calculated
from the input set of vectors. The class %PCA can also transform
vectors to/from the new coordinate space defined by the basis. Usually,
in this new coordinate system, each vector from the original set (and
any linear combination of such vectors) can be quite accurately
approximated by taking its first few components, corresponding to the
eigenvectors of the largest eigenvalues of the covariance matrix.
Geometrically it means that you calculate a projection of the vector to
a subspace formed by a few eigenvectors corresponding to the dominant
eigenvalues of the covariance matrix. And usually such a projection is
very close to the original vector. So, you can represent the original
vector from a high-dimensional space with a much shorter vector
consisting of the projected vector's coordinates in the subspace. Such a
transformation is also known as Karhunen-Loeve Transform, or KLT.
See http://en.wikipedia.org/wiki/Principal_component_analysis
*/
enum Flags { DATA_AS_ROW = 0, //!< indicates that the input samples are stored as matrix rows
             DATA_AS_COL = 1, //!< indicates that the input samples are stored as matrix columns
             USE_AVG     = 2  //!
           };
/** @overload
@param data input samples stored as matrix rows or matrix columns.
@param mean optional mean value; if the matrix is empty (@c noArray()),
the mean is computed from the data.
@param flags operation flags; currently the parameter is only used to
specify the data layout (PCA::Flags)
@param maxComponents maximum number of components that %PCA should
retain; by default, all the components are retained.
*/
PCA(InputArray data, InputArray mean, int flags, int maxComponents = 0);

```
- Save mean vector
<img src="https://render.githubusercontent.com/render/math?math=M_{dx1}">
- Save eigenvectors matrix
<img src="https://render.githubusercontent.com/render/math?math=E_{lxd}">
- All done


## Testing
- Read labeled sample face images
- Read Testing images
- Transform  labeled sample face image matrixs to row vectors data DS

<img src="https://render.githubusercontent.com/render/math?math=DS_{dxk}">
- Transform testing image matrixs to row vectors data DT
<img src="https://render.githubusercontent.com/render/math?math=DT_{dxm}">
- Read mean vector
<img src="https://render.githubusercontent.com/render/math?math=M_{dx1}"> 
- For each row of data DS,subtracting mean vector to normalize 
- For each row of data DL,subtracting mean vector to normalize 
- Read eigenvectors matrix
<img src="https://render.githubusercontent.com/render/math?math=E_{lxd}">
- Caculate the eigen of sample face datas row vectors DSe
<img src="https://render.githubusercontent.com/render/math?math=DSe_{lxk}=E_{lxd}*DS_{dxk}">
- For each row in testing image row vectors data DT,caculate the eigen
<img src="https://render.githubusercontent.com/render/math?math=de_{lx1}=E_{lxd}*d_{dx1}">
- Find the nearest Euclidean distance of de and row in DSe

# (4)Benchmarking with different Eigenvalues Quantity



# (5)Boosting-1,Use KNN

# (6)Boosting-2,Adjust Test/Train Sample Ratio

# (7)Summary and To Do Next
