# Python Library API

## Causal Relationship Discovery

### ensemble

inference by heterogenous parallel base-estimators

def ensemble(data:pd.DataFrame)->List\[np.ndarray\]:

**Inputs**

-   data: pd.DataFrame, i.e. the Time-independent steady-state system or
    experimental cross section data obtained by randomized statistics. 

    |   |  A  |  B  |  C  |
    | ---- | ---- | ---- | ---- |
    | 1 | 18.5 | 129.5 | 243 |
    | 2 | 56 | 492.5 | 1426 |
    | 3 | 250.5 | 2769 | 14043.5 |

**Outputs**

-   candidates: List\[np.ndarray\], i.e. the outputs of multiple base-e
    stimators(AKA constraint-based, score-based, permutation-based,
    linear Gaussian acyclic, continuous optimization)

### voting

Soft voting machines that integrate basic estimates

def voting(candidates:List\[np.ndarray\], priori:pd.DataFrame)->np.ndarray:

**Inputs**

-   candidates: List\[np.ndarray\], i.e. the return value of ensemble

-   priori: np.ndarray, i.e.adjcency_matrix of partial graph containing
    priori knowledge

**Outputs**

-   fine_graph: the predicted causal directed graph

## Given Graph Falsification

### falsifypack

**Inputs**

-   data_path: str. The file format should be csv. The file content
    format should be similar to Table 1

-   graph_path: str. The file format should be gml. GML, the Graph
    Modelling Language. A GML file consists of a hierarchical key-value
    lists. Graphs can be annotated with arbitrary data structures. GML
    is the standard file format in the Graphlet graph editor system.

-   to_plot: boolean. True for plotting the permutation-fraction of
    violations figure

-   significance_level = 0.05: float. Significance level for the
    permutation test.

-   significance_ci = 0.05: float. Significance level for (conditional)
    independence tests.

-   n_perm = 100: int. Number of permutations to perform. If -1 use all
    n_nodes! permutations.

**Outputs**

-   results: str, i.e. text blob of Falsificaton Summary which contains
    a set of metrics.

## Kink & Discontinuity Regression

### kink_regression_2d
use local piecewise linear regression to realize kink regression and
discontinuous regression, which applys to timeseries data and common x-y
data

**Inputs**

-   file_path:str, i.e. path to timeseries data and common x-y data.
    file format: .csv

-   xl: float. local regression lower x-bound

-   xh: float. local regression upper x-bound

-   iplot: boolean. True for plotting the x-y regression figure

**Outputs**

-   best_knot_x: the x-coordinate of kink with lowest residual error

-   best_model: an object of piecewise regression model class

### kink_regression_3d
use local piecewise linear regression of higher dimension to realize
kink regression and discontinuous regression, which applys to x-y-target
data

**Inputs**

-   file_path: str, i.e. path to common x-y-z data. file format: .csv

-   xl, xh, yl, yh: float, i.e. local regression lower and upper
    xy-bound

-   iplot: boolean. True for plotting the regression figure

-   response_surface_design: boolean. True for build response surface

**Outputs**

-   best_knot_x,best_knot_y: the xy-coordinate of kink with lowest
    residual error

-   best_model: an object of piecewise regression model class

-   filtered_data: points of O(mintarget) in the response surface, if
    response_surface_design == True

## Response Surface Methodology

### bayes_opt

def bayes_opt(df:pd.DataFrame, ploy_dim=2, init_p=5, iters=25,
verbose\_=2, mode='maximize'):

**Inputs**

-   df: pd.DataFrame with columns "X", "Y", "Z".

-   ploy_dim: Degree of polynomial surrogate model

-   init_p: Number of random points to probe before starting the
    optimization.

-   iters: Number of iterations where the method attempts to find the
    maximum value.

-   verbose\_: The level of verbosity. verbose = 2 prints all probed
    points, verbose = 1 prints only when a maximum is observed, verbose
    = 0 is silent.

-   mode: str. 'maximize' or 'minimize'

**Outputs**

-   results: json. {'target':_, 'params': {'x':_, 'y': _}}

## Input-Output Module

### load_data
**Inputs**

-   path: str, i.e. the relative or absolute path of data file to the
    current directory

-   type: str, i.e. the type of the file. Supported types include 'csv',
    'gse', 'e-mtab' , which refer to common .csv-like file, GEO "Series
    Matrix File(s)" and ArrayExress "E-MTAB" respectively.

**Return**

-   processed_data: DataFrame, i.e. legal data to calculate by the above
    functions and to be accepted by the API of the python library

### array_to_gml
**Inputs**

-   arr: np.ndarray, i.e. the adjacency matrix of causal graph

-   file_name: str, i.e. the name of the file saved in the current dir.

-   labels: list\[str\], i.e. a 3x3 array represents 3 nodes
    \['A','B','C'\]

**Outputs**

-   file: .gml. GML, the Graph Modelling Language. GML's key features
    are portability, simple syntax, extensibility and flexibility. A GML
    file consists of a hierarchical key-value lists. Graphs can be
    annotated with arbitrary data structures. The idea for a common file
    format was born at the GD'95; this proposal is the outcome of many
    discussions. GML is the standard file format in the Graphlet graph
    editor system. It has been overtaken and adapted by several other
    systems for drawing graphs.

### gml_to_array
**Inputs**

-   file_path: .gml. GML, the Graph Modelling Language. A GML file
    consists of a hierarchical key-value lists. Graphs can be annotated
    with arbitrary data structures. GML is the standard file format in
    the Graphlet graph editor system.

**Return**

-   array: np.ndarray, i.e. the adjacency matrix of causal graph
