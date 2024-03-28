# A Comprehensive Tutorial of Regularization 3D Plot

## Table of Contents

- [Introduction](#introduction)
- [Environment Setup](#environment-setup)
- [Installation Instructions](#installation-instructions)
- [Evaluation](#evaluation)
- [Resources](#resources)
- [License](#license)
- [Conclusion](#conclusion)
- [About Author](#about-author)

## Introduction

Dive into the world of regularization with my tutorial, featuring Ridge regression (L2 penalty) and LASSO regression (L1 penalty). Explore Mean Squared Error (MSE) contours, visualize the impact of collinearity, and uncover how L1 and L2 penalties shape model complexity. Prepare to gain deeper insights into regularization methods through concise explanations and 3D visualizations. Enhance your understanding and application of these techniques with my comprehensive guide.


## Environment Setup

**Prerequisites**: Ensure Python 3.6 or newer is installed on your system.

1. **Create a Virtual Environment**:
    - Install `virtualenv` if you prefer it over the built-in `venv` (optional):
        ```bash
        pip install virtualenv
        ```
    - Create the environment:
        - With `venv` (Python 3.3+):
            ```bash
            python -m venv env
            ```
        - Or, with `virtualenv`:
            ```bash
            virtualenv env
            ```
    - Activate the environment:
        - Windows: `env\Scripts\activate`
        - Unix/MacOS: `source env/bin/activate`
    - To deactivate: `deactivate`

2. **Dependencies**:
    Ensure all dependencies are listed in `requirements.txt`. Install them using:
    ```bash
    pip install -r requirements.txt
    ```

## Installation Instructions

To use this project, clone the repository and set up the environment as follows:

1. **Clone the Repository**:
    ```bash
    https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot.git
    ```
2. **Setup the Environment**:
    - Navigate to the project directory and activate the virtual environment.
    - Install the dependencies from `requirements.txt`.

## Evaluation

### Collinearity

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/672ee1d3-e4ca-4944-9224-3100346d4ec0)

We can clearly see the collinearity in the pairplot.

### MSE contours with collinearity

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/61a0f9ce-829d-4fc8-b3a5-4fb2f149863f)

On both contour plots, the dark red region shows the combination of coefficients where MSE is smallest, and the star marks the “true” coefficients.

- On the right, with two independent features, all of the combinations of coefficients that have small MSE are fairly similar.
- On the left, with collinear features, we can see that the region with small MSE spans a broad range of coefficient values. The region appears as a long, narrow “valley” in the MSE contour. (If you would plot a “higher is better” metric, such as R2, instead of a “lower is better” metric like MSE, you would see a long, narrow “ridge” (Ridge!!!) in the contour plot!)
  
We can see that with collinear features, a small change in the training data could cause the pair of coefficient values that have the smallest MSE - the least squares estimate - to move anywhere along the “valley”. The model will have much more variance due to the much larger range of likely coefficient estimates.

### Simulation: collinear features

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/97ffa21d-e59c-40dd-9978-1063843514b4)

The individual orange lines in the two top subplots show the predictions of the model when it is trained on each of the many independent training sets.

Note that for Model A, on the left, all the orange lines are similar - the predictions on the test set are similar for all the different training sets (low variance).

For Model B, on the right, the different training sets lead to very different coefficient estimates, and therefore, high variance in the model estimates.


### MSE contours with L2 penalty

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/8ea894da-a8b1-419b-9ef5-a30ce1120b99)

When there are collinear features, there are very different coefficient estimates that all have similar MSE. The coefficient estimate is very unstable, so the model has high variance.

To reduce the variance, we want to make sure that the training algorithm selects similar coefficients every time, even when there are slight differences in the training data.

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/9bdd0aa8-3c91-4b47-87ce-621b30c5988a)

The MSE term in the loss function tends to push our coefficient estimates towards the “true” coefficients, in the center of the dark red region. At the same time, the L2 penalty term tends to push our coefficient estimate towards the origin. The α parameter determines the relative strength of each effect.

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/0272595a-3f4e-45c3-a12a-add2e0e43b1d)

In both cases, the regularized loss function shrinks the region of coefficients for which the loss function is very small - the region of likely coefficient estimates.

In the case with collinear features, though, the range of coefficients with small loss shrinks dramatically due to regularization. The L2 penalty term “pulls up” on the parts of the “ridge” that are far from the origin, increasing the value of the loss function there. The long, narrow “ridge” becomes a small peak, and the coefficient estimates are now much more stable.

However, the “true” coefficients may no longer be included in the region where the value of the loss function is smallest - the L2 penalty introduces bias, moving the coefficient estimate away from the true value.

### Simulation: L2 penalty

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/7a55c0db-57db-47b9-80c1-fdd5139f6f1c)

### Simulation: uninformative features

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/aa932c7b-54f8-4fc7-8901-a2321cc1ae09)

### Simulation: L1 penalty

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/e7673e2e-3f44-47e8-a0be-1c6cde11886c)

### MSE contours with L1 penalty

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/f76ad050-a5e0-48a4-9b31-a87d5b7b2c4b)

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/6032d859-947d-47f4-a154-4a7caa9d594a)

![image](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot/assets/149146155/dc00d8f8-e5ba-4256-ab38-52e6e28b3110)



## Resources

- **Kaggle Notebook**: [View Notebook](https://www.kaggle.com/code/muhammadimran112233/a-comprehensive-tutorial-of-regularization-3d-plot)

## License

This project is made available under the MIT License.

## Conclusion

Through my comprehensive tutorial on regularization 3D plots, we've delved into the intricacies of Ridge and LASSO regression. By visualizing MSE contours and exploring the effects of L1 and L2 penalties, we've gained valuable insights into model complexity and performance.

You're now equipped to leverage regularization techniques effectively in your machine learning projects. Whether mitigating collinearity or optimizing model complexity, regularization 3D plots offer a powerful tool for enhancing model performance and interpretability.

## About Author

- **Name**: Muhammad Imran Zaman
- **Email**: [imranzaman.ml@gmail.com](mailto:imranzaman.ml@gmail.com)
- **Professional Links**:
    - Kaggle: [Profile](https://www.kaggle.com/muhammadimran112233)
    - LinkedIn: [Profile](linkedin.com/in/muhammad-imran-zaman)
    - Google Scholar: [Profile](https://scholar.google.com/citations?user=ulVFpy8AAAAJ&hl=en)
    - YouTube: [Channel](https://www.youtube.com/@consolioo)
- **Project Repository**: [GitHub Repo](https://github.com/Imran-ml/A-Comprehensive-Tutorial-of-Regularization-3D-Plot.git)
