LIBOKL-- A Library for Online Kernel Learning Algorithms

Authors:
Lu Jing, Wu Yue, Steven Hoi

Contact: chhoi@ntu.edu.sg, jing.lu.2014@phdis.smu.edu.sg

LIBOKL is a package for solving large scale online kernel learning tasks. The current version is in C++ and has a total of 10 different online single kernel learning algorithm for binary classification, which are all widely used in online kernel learning research. We also provide other packages for multi-class classification and regression and multiple kernel learning. See the link at the end.

The algorithms in this package includes:

1. Perceptron: The kernelized Perceptron without budget maintainance. http://cseweb.ucsd.edu/~yfreund/papers/LargeMarginsUsingPerceptron.pdf

2. Online Gradient Descent (OGD): The kernelized online gradient descent algorithm without budget maintainance. 
http://eprints.pascal-network.org/archive/00002055/01/KivSmoWil04.pdf

3. Random Budget Perceptron (RBP): Budgeted perceptron algorithm with random support vector removal strategy. 
 http://air.unimi.it/bitstream/2434/26350/1/J29.pdf

4. Forgetron: Forgetron algorithm that maintains the budget size by discarding the oldest support vectors. 
http://papers.nips.cc/paper/2806-the-forgetron-a-kernel-based-perceptron-on-a-fixed-budget.pdf

5. Projectron: The Projectron algorithm using budget projection strategy. 
http://eprints.pascal-network.org/archive/00004472/01/355.pdf

6. Projectron++: The aggressive version of Projectron algorithm that updates with both margin error and mistake case. 
http://eprints.pascal-network.org/archive/00004472/01/355.pdf

7. BPAs: The budget passive-aggressive algrotihtm with simple supprot removal strategy.
http://machinelearning.wustl.edu/mlpapers/paper_files/AISTATS2010_WangV10.pdf

8. BOGD: The budget online gradient descent algorithm by SV removal strategy 
http://arxiv.org/ftp/arxiv/papers/1206/1206.4633.pdf

9. FOGD: The Fourier Online Gradient Descent algorithm using functional approximation method.
http://jingonline.weebly.com/uploads/5/3/7/3/53733905/lu15a.pdf

10. NOGD: The Nystrom Online Gradient Descent algorithm using functional approximation method.[pdf]
http://jingonline.weebly.com/uploads/5/3/7/3/53733905/lu15a.pdf

The last two were proposed by our group and published on Journal of Machine Learning Research. If you need to use this code package, please cite our paper as: 
________________________________________

Lu J, Hoi S C H, Wang J, et al. Large scale online kernel learning[J]. Journal of Machine Learning Research, 2016, 17(47): 1.

or bib:
________________________________________
@article{lu2016large,
  title={Large scale online kernel learning},
  author={Lu, Jing and Hoi, Steven CH and Wang, Jialei and Zhao, Peilin and Liu, Zhi-Yong},
  journal={Journal of Machine Learning Research},
  volume={17},
  number={47},
  pages={1},
  year={2016},
  publisher={Journal of Machine Learning Research/Microtome Publishing}
}
_________________________________________

We will birefly introduce the usage of LIBOKL. To get started, please refer to the file install.pdf, which provide a detailed step-by-step guide on the installation of this package. Before it, an Eigen package is needed (http://eigen.tuxfamily.org/index.php?title=Main_Page). After building, we get an executable file KOL and use it in command line.
_______________________________________

Prepare for the input data

We use the LIBSVM dataset formate, which is an effcient sparse data representation as input.  Each instance in the dataset is represented by a row of numbers ended by "\n". For example:

+1 5:1 16:1 20:1 37:1 40:1 63:1 68:1 73:1 74:1 76:1 82:1 93:1

-1 2:1 6:1 18:1 19:1 39:1 40:1 52:1 61:1 71:1 72:1 74:1 76:1 80:1 95:1

In the above dataset, there are 2 instances stored in two rows. Each row begins with the class label of this instance. In binary classification the label appears in two forms: {+1, -1}. Note that some dataset files might be labeled with {0, 1}, which is not allowed by our toolbox. They have to be preprocessed and transformed to the {-1,+1} formate. Following the label, the feature values appears in form feature_index:feature_value. This is a sparse feature representation. If one certain feature index does not appear, it indicates that its value is zero.

Our toolbox is well designed to follow the standard online learning setting and load the dataset sequentially. So there is no memory limitation at all for large scale datasets. Users are not required to input the feature dimension of the dataset before training, since the algorithm will automaticly adjust to the increase of feature dimension.

_________________________________

Command Line

After compiling the code of the toolbox and getting the executable file "KOL", we can use command line mode to run the algorithms:

>>KOL -i training_dataset [-t testing_dataset] -opt algorithm_name [parameter setting]

KOL is the name of the executable file we got from compiling the code. -i training_dataset is a necessary input indicating the training dataset name. -opt algorithm_name is another necessary input indicating the selected algorithm for learning. -t testing_dataset is an optional input indicating the testing dataset name. If not indicated, the algorithm will only conduct the training process and output the online training accuracy and time cost. Parameter setting is also optional and diverses among different algorithms. If not indicated, the algorithm will use default setting.

______________________________________

A quick example:

We may download the a9a datasets and perform the online kernel learning using the perceptron algorithm. We try the following command line:

>>KOL -i a9a_train -t a9a_test -opt kernel-perceptron

The ourput is as followings:

Algorithm: kernel_perceptron 
0	10000	20000	30000 
#Training Instances:32561
Learn acuracy: 78.851997%
#SV:6887
Learning time: 10.218000 s
Test acuracy: 70.738899 %
Test time: 9.766000 s

The second line indicates the number of processed training samples until now, which can give an intuitive impression of the processing speed. This is a necessary output in the case when the training time is extremely long. The output includes the training accuracy, training time cost (including loading time), the number of support vectors, test accuracy and test time (including loading time).

__________________________________________________________



