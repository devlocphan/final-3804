# Data Mining with Python

Source: [week 1 lab.pdf](../week%201%20lab.pdf)

## Slide 1

### Data Mining with Python

Dr Can Wang

## Slide 2

### Data Mining Tools Ranking

| Data Mining Tool | 2017 | 2016 | 2015 | 2014 |
| --- | --- | --- | --- | --- |
| R | 52% | 49% | 46.9% | 38.5% |
| RapidMiner | 32.8% | 32.6% | 31.5% | 44.2% |
| SQL | 34.9% | 35.5% | 30.9% | 25.3% |
| Python | 52.6% | 45.8% | 30.3% | 19.5% |
| Excel | 28.1% | 33.6% | 22.9% | 25.8% |
| KNIME | 19.1% | 18.0% | 20.0% | 15.0% |
| Hadoop | 15.0% | 22.1% | 18.4% | 12.7% |
| Tableau | 19.4% | 18.5% | 12.4% | 9.1% |
| SAS | — | 5.6% | 11.3% | 10.9% |
| Spark | 22.7% | 21.6% | 11.3% | 2.6% |

Top 10 most popular free data mining tools, surveyed by data mining experts at Kdnuggets.com from thousands of readers.

**TIOBE Programming Community Index**

[Figure: July 2021 programming-language rankings and a historical popularity line chart spanning approximately 2002–2021. OCR recovered the leading languages C, Java, Python, C++, C#, Visual Basic, JavaScript, and PHP. The Python chart tooltip reads “Sunday, Jul 4, 2021; Python: 10.95%”. Small ranking/change values and plot details are only partly recovered.]

| July 2021 rank | Language | Rating (OCR) |
| --- | --- | --- |
| 1 | C | 11.62% |
| 2 | Java | 11.17% |
| 3 | Python | 10.95% |
| 4 | C++ | 8.01% |
| 5 | C# | 4.83% |
| 6 | Visual Basic | 4.50% |
| 7 | JavaScript | 2.71% |
| 8 | PHP | 2.58% |

## Slide 3

### Python Libraries for Data Mining

- **NumPy** stands for Numerical Python. The most powerful feature of NumPy is n-dimensional array. This library also contains basic linear algebra functions, Fourier transforms, advanced random number capabilities and tools for integration with other low-level languages like Fortran, C and C++.
- **SciPy** stands for Scientific Python. SciPy is built on NumPy. It is one of the most useful library for variety of high-level science and engineering modules like discrete Fourier transform, Linear Algebra, Optimization and Sparse matrices.
- **Pandas** is for structured data operations and manipulations. It is extensively used for data munging and preparation. Pandas were added relatively recently to Python and have been instrumental in boosting Python's usage in data scientist community.
- **Scikit Learn** is for machine learning. Built on NumPy, SciPy and matplotlib, this library contains a lot of efficient tools for machine learning and statistical modeling including classification, regression, clustering and dimensionality reduction.
- **Matplotlib** is for plotting vast variety of graphs, starting from histograms to line plots to heat plots. You can use Pylab feature in ipython notebook (`ipython notebook –pylab = inline`) to use these plotting features inline. If you ignore the inline option, then pylab converts ipython environment to an environment, very similar to Matlab. You can also use Latex commands to add math to your plot.
- **Seaborn** is for statistical data visualization. Seaborn is a library for making attractive and informative statistical graphics in Python. It is based on matplotlib. Seaborn aims to make visualization a central part of exploring and understanding data.
- **Scrapy** is for web crawling. It is a very useful framework for getting specific patterns of data. It has the capability to start at a website home URL and then dig through web-pages within the website to gather information.
- And more …

## Slide 4

### Jupyter Notebook (1)

- The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations (LaTeX supported), visualizations and narrative text.
- Uses include: data cleaning and transformation, numerical simulation, statistical modelling, data visualization, machine learning, and much more.
- The Notebook has support for over 40 programming languages, including Python, R, Julia, and Scala.
- Notebooks can be shared with others using email, Dropbox, GitHub and the Jupyter Notebook Viewer.
- Your code can produce rich, interactive output: HTML, images, videos, LaTeX, and custom MIME types.
- Leverage big data tools, such as Apache Spark, from Python, R and Scala. Explore that same data with pandas, scikit-learn, ggplot2, TensorFlow.

## Slide 5

### Jupyter Notebook (2)

- Run Jupyter Notebooks With the Anaconda Python Distribution.
- One of the requirements here is Python. The general recommendation is that you use the Anaconda distribution to install both Python and the notebook application.
- The advantage of Anaconda is that you have access to over 720 packages that can easily be installed with Anaconda's conda, a package, dependency, and environment manager. You can download and follow the instructions for the installation of Anaconda: https://www.anaconda.com/download/.

[Figure: Anaconda download-page screenshot, headed “Download Anaconda Distribution”; decorative/web-interface details are not reproduced.]

## Slide 6

### Jupyter Notebook (3)

- Getting Started With Jupyter Notebook.
- Run the following command to open up the application:

```bash
jupyter notebook
```

- Then you'll see the application opening in the web browser on the following address: http://localhost:8888.

[Figure: terminal screenshot demonstrating the command above; machine-specific shell text is not reproduced.]

## Slide 7

### Jupyter Notebook (4)

[Figure: Jupyter dashboard file browser. Tabs: Files, Running, Clusters. Controls: Upload, New, select items to perform actions. Breadcrumb: research / doc. Listed entries include lstms, test, att, liblinear_coderead.txt, and libsvm_coderead.txt; one entry is marked Running. Small timestamps and one filename are unclear after OCR.]

## Slide 8

### Jupyter Notebook (5)

[Figure: example notebook titled “jupyter tutorial”, last checkpoint 06/26/2018, unsaved changes, Python 3, Not Trusted. Menus: File, Edit, View, Insert, Cell, Kernel, Widgets, Help. It mixes Markdown, Python code, output, headings, and a formula.]

Text recovered from the screenshot:

- “This doc is my first Jupyter sample.”
- A simple-operation cell has output `5`; the input expression is not reliably recovered.
- “Counter”:

```python
a = [i for i in range(15)]
print(a)
```

```text
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

- “this code is for testing”
- “this heading is first”
  - “this heading is second”
    - “this heading is third”
- A final displayed formula begins `a+b=`; its remainder is unclear after OCR.

A good basic tutorial of Jupyter Notebook:

https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook

## Slide 9

### Reference

- https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook
- https://www.analyticsvidhya.com/blog/2016/01/complete-tutorial-learn-data-science-python-scratch-2/
