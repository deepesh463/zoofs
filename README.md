# zoofs
![zoofs Logo Header](https://github.com/jaswinder9051998/zoofs/blob/master/asserts/zoofsedited.png)

``zoofs`` is a Python library for performing feature selection using an variety of nature inspired wrapper algorithms. The algorithms range from swarm-intelligence to physics based to Evolutionary. 
It's easy to use ,flexible and powerful tool to reduce your feature size.  

## Installation

### Using pip

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install zoofs.

[![PyPi Downloads]()]()
[![PyPi Version]()]()

```bash
pip install zoofs
```

## Available Algorithms 
| Algorithm Name | Class Name | Description |
|----------|-------------|-------------|
| Particle Swarm Algorithm  | ParticleSwarmOptimization | Utilizes swarm behaviour |
| Grey Wolf Algorithm | GreyWolfOptimization | Utilizes wolf hunting behaviour |
| Dragon Fly Algorithm | DragonFlyOptimization | Utilizes dragonfly swarm behaviour |
| Genetic Algorithm Algorithm | GeneticOptimization | Utilizes genetic mutation behaviour |
| Gravitational Algorithm | GravitationalOptimization | Utilizes newtons gravitational behaviour |

* [Try It Now?] [![Open In Colab](https://camo.githubusercontent.com/52feade06f2fecbf006889a904d221e6a730c194/68747470733a2f2f636f6c61622e72657365617263682e676f6f676c652e636f6d2f6173736574732f636f6c61622d62616467652e737667)]() 

## Usage
Define your own objective function for optimization !
```python
from sklearn.metrics import log_loss
# define your own objective function, make sure the function receives four parameters,
#  fit your model and return the objective value ! 
def objective_function_topass(model,X_train, y_train, X_valid, y_valid):      
    model.fit(X_train,y_train)  
    P=log_loss(y_valid,model.predict_proba(X_valid))
    return P
    
# import an algorithm !  
from zoofs import ParticleSwarmOptimization
# create object of algorithm
algo_object=ParticleSwarmOptimization(objective_function_topass,n_iteration=20,
                                       population_size=20,minimize=True)
import lightgbm as lgb
lgb_model = lgb.LGBMClassifier()                                       
# fit the algorithm
algo_object.fit(lgb_model,X_train, y_train, X_valid, y_valid,verbose=True)
#plot your results
algo_object.plot_history()
   
```
 <br/>
 <br/>
 
## Algorithms 

### _Particle Swarm Algorithm_
![Particle Swarm](https://media.giphy.com/media/tBRQNyh6fKBpSy2oif/giphy.gif)

------------------------------------------
#### class zoofs.ParticleSwarmOptimization(objective_function,n_iteration=50,population_size=50,minimize=True,c1=2,c2=2,w=0.9)
------------------------------------------

|  |  |
|----------|-------------|
|  Parameters  | ``objective_function`` :  user made function of the signature 'func(model,X_train,y_train,X_test,y_test)'. <br/> <dl> <dd> The function must return a value, that needs to be minimized/maximized. </dd> </dl> ``n_iteration ``: int, default=50 <br/> <dl> <dd> Number of time the algorithm will run  </dd> </dl> ``population_size`` : int, default=50 <br/> <dl> <dd> Total size of the population  </dd> </dl> ``minimize ``: bool, default=True <br/> <dl> <dd> Defines if the objective value is to be maximized or minimized </dd> </dl> ``c1`` : float, default=2.0 <br/> <dl> <dd> first acceleration coefficient of particle swarm  </dd> </dl>    ``c2`` : float, default=2.0 <br/> <dl> <dd> second acceleration coefficient of particle swarm  </dd> </dl> `w` : float, default=0.9 <br/> <dl> <dd> weight parameter  </dd> </dl>| 
| Attributes | ``best_feature_list`` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### Methods

| Methods | Class Name |
|----------|-------------|
|  fit  | Run the algorithm  | 
| plot_history | Plot results achieved across iteration |

#### fit(model,X_train, y_train, X_test, y_test,verbose=True)

|  |  |
|----------|-------------|
|   Parameters | ``model`` : <br/> <dl> <dd> machine learning model's object </dd> </dl> ``X_train`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/><dl> <dd> Training input samples to be used for machine learning model </dd> </dl> ``y_train`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples) <br/> <dl> <dd> The target values (class labels in classification, real numbers in regression). </dd> </dl> ``X_valid`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/> <dl> <dd> Validation input samples </dd> </dl> ``y_valid`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples)  <br/> <dl> <dd> The Validation target values . </dd> </dl> ``verbose`` : bool,default=True  <br/> <dl> <dd> Print results for iterations </dd> </dl>| 
| Returns  | ``best_feature_list `` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### plot_history()
Plot results across iterations

#### Example 
```python
from sklearn.metrics import log_loss
# define your own objective function, make sure the function receives four parameters,
#  fit your model and return the objective value ! 
def objective_function_topass(model,X_train, y_train, X_valid, y_valid):      
    model.fit(X_train,y_train)  
    P=log_loss(y_valid,model.predict_proba(X_valid))
    return P
    
# import an algorithm !  
from zoofs import ParticleSwarmOptimization
# create object of algorithm
algo_object=ParticleSwarmOptimization(objective_function_topass,n_iteration=20,
                                       population_size=20,minimize=True,c1=2,c2=2,w=0.9)
import lightgbm as lgb
lgb_model = lgb.LGBMClassifier()                      
# fit the algorithm
algo_object.fit(lgb_model,X_train, y_train, X_valid, y_valid,verbose=True)
#plot your results
algo_object.plot_history()
```  
<br/>
<br/>

### _Grey Wolf Algorithm_
![Grey Wolf](https://media.giphy.com/media/CvgezXSuQTMTC/giphy.gif)

------------------------------------------
#### class zoofs.GreyWolfOptimization(objective_function,n_iteration=50,population_size=50,minimize=True)
------------------------------------------
|  |  |
|----------|-------------|
|  Parameters  | ``objective_function`` :  user made function of the signature 'func(model,X_train,y_train,X_test,y_test)'. <br/> <dl> <dd> The function must return a value, that needs to be minimized/maximized. </dd> </dl> ``n_iteration ``: int, default=50 <br/> <dl> <dd> Number of time the algorithm will run  </dd> </dl> ``population_size`` : int, default=50 <br/> <dl> <dd> Total size of the population  </dd> </dl> ``minimize ``: bool, default=True <br/> <dl> <dd> Defines if the objective value is to be maximized or minimized </dd> </dl>| 
| Attributes | ``best_feature_list`` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### Methods

| Methods | Class Name |
|----------|-------------|
|  fit  | Run the algorithm  | 
| plot_history | Plot results achieved across iteration |

#### fit(model,X_train,y_train,X_valid,y_valid,method=1,verbose=True)

|  |  |
|----------|-------------|
|   Parameters | ``model`` : <br/> <dl> <dd> machine learning model's object </dd> </dl> ``X_train`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/><dl> <dd> Training input samples to be used for machine learning model </dd> </dl> ``y_train`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples) <br/> <dl> <dd> The target values (class labels in classification, real numbers in regression). </dd> </dl> ``X_valid`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/> <dl> <dd> Validation input samples </dd> </dl> ``y_valid`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples)  <br/> <dl> <dd> The Validation target values . </dd> </dl> ``method`` : {1, 2}, default=1 <br/> <dl> <dd> Choose the between the two methods of grey wolf optimization </dd> </dl>``verbose`` : bool,default=True  <br/> <dl> <dd> Print results for iterations </dd> </dl>| 
| Returns  | ``best_feature_list `` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### plot_history()
Plot results across iterations

#### Example 
```python
from sklearn.metrics import log_loss
# define your own objective function, make sure the function receives four parameters,
#  fit your model and return the objective value ! 
def objective_function_topass(model,X_train, y_train, X_valid, y_valid):      
    model.fit(X_train,y_train)  
    P=log_loss(y_valid,model.predict_proba(X_valid))
    return P
    
# import an algorithm !  
from zoofs import GreyWolfOptimization
# create object of algorithm
algo_object=GreyWolfOptimization(objective_function_topass,n_iteration=20,
                                    population_size=20,minimize=True)
import lightgbm as lgb
lgb_model = lgb.LGBMClassifier()                                       
# fit the algorithm
algo_object.fit(lgb_model,X_train, y_train, X_valid, y_valid,method=1,verbose=True)
#plot your results
algo_object.plot_history()
```  
<br/>
<br/>

### _Dragon Fly Algorithm_
![Dragon Fly](https://media.giphy.com/media/xTiTnozh5piv13iFBC/giphy.gif)

------------------------------------------
#### class zoofs.DragonFlyOptimization(objective_function,n_iteration=50,population_size=50,minimize=True)
------------------------------------------
|  |  |
|----------|-------------|
|  Parameters  | ``objective_function`` :  user made function of the signature 'func(model,X_train,y_train,X_test,y_test)'. <br/> <dl> <dd> The function must return a value, that needs to be minimized/maximized. </dd> </dl> ``n_iteration ``: int, default=50 <br/> <dl> <dd> Number of time the algorithm will run  </dd> </dl> ``population_size`` : int, default=50 <br/> <dl> <dd> Total size of the population  </dd> </dl> ``minimize ``: bool, default=True <br/> <dl> <dd> Defines if the objective value is to be maximized or minimized </dd> </dl>| 
| Attributes | ``best_feature_list`` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### Methods

| Methods | Class Name |
|----------|-------------|
|  fit  | Run the algorithm  | 
| plot_history | Plot results achieved across iteration |

#### fit(model,X_train,y_train,X_valid,y_valid,method='sinusoidal',verbose=True)

|  |  |
|----------|-------------|
|   Parameters | ``model`` : <br/> <dl> <dd> machine learning model's object </dd> </dl> ``X_train`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/><dl> <dd> Training input samples to be used for machine learning model </dd> </dl> ``y_train`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples) <br/> <dl> <dd> The target values (class labels in classification, real numbers in regression). </dd> </dl> ``X_valid`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/> <dl> <dd> Validation input samples </dd> </dl> ``y_valid`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples)  <br/> <dl> <dd> The Validation target values . </dd> </dl> ``method`` : {'linear','random','quadraic','sinusoidal'}, default='sinusoidal' <br/> <dl> <dd> Choose the between the three methods of Dragon Fly optimization </dd> </dl>``verbose`` : bool,default=True  <br/> <dl> <dd> Print results for iterations </dd> </dl>| 
| Returns  | ``best_feature_list `` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### plot_history()
Plot results across iterations

#### Example 
```python
from sklearn.metrics import log_loss
# define your own objective function, make sure the function receives four parameters,
#  fit your model and return the objective value ! 
def objective_function_topass(model,X_train, y_train, X_valid, y_valid):      
    model.fit(X_train,y_train)  
    P=log_loss(y_valid,model.predict_proba(X_valid))
    return P
    
# import an algorithm !  
from zoofs import DragonFlyOptimization
# create object of algorithm
algo_object=DragonFlyOptimization(objective_function_topass,n_iteration=20,
                                    population_size=20,minimize=True)
import lightgbm as lgb
lgb_model = lgb.LGBMClassifier()                                     
# fit the algorithm
algo_object.fit(lgb_model,X_train, y_train, X_valid, y_valid, method='sinusoidal', verbose=True)
#plot your results
algo_object.plot_history()
```  
<br/>
<br/>

### _Genetic Algorithm_
![Dragon Fly](https://media.giphy.com/media/3o85xGrC7nPVbA2y3K/giphy.gif)

------------------------------------------
#### class zoofs.GeneticOptimization(objective_function,n_iteration=20,population_size=20,selective_pressure=2,elitism=2,mutation_rate=0.05,minimize=True)
------------------------------------------
|  |  |
|----------|-------------|
|  Parameters  | ``objective_function`` :  user made function of the signature 'func(model,X_train,y_train,X_test,y_test)'. <br/> <dl> <dd> The function must return a value, that needs to be minimized/maximized. </dd> </dl> ``n_iteration``: int, default=50 <br/> <dl> <dd> Number of time the algorithm will run  </dd> </dl> ``population_size`` : int, default=50 <br/> <dl> <dd> Total size of the population  </dd> </dl> ``selective_pressure``: int, default=2 <br/> <dl> <dd>measure of reproductive opportunities for each organism in the population </dd> </dl> ``elitism``: int, default=2 <br/> <dl> <dd> number of top individuals to be considered as elites </dd> </dl> ``mutation_rate``: float, default=0.05 <br/> <dl> <dd> rate of mutation in the population's gene </dd> </dl> ``minimize``: bool, default=True <br/> <dl> <dd> Defines if the objective value is to be maximized or minimized </dd> </dl>| 
| Attributes | ``best_feature_list`` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### Methods

| Methods | Class Name |
|----------|-------------|
|  fit  | Run the algorithm  | 
| plot_history | Plot results achieved across iteration |

#### fit(model,X_train,y_train,X_valid,y_valid,verbose=True)

|  |  |
|----------|-------------|
|   Parameters | ``model`` : <br/> <dl> <dd> machine learning model's object </dd> </dl> ``X_train`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/><dl> <dd> Training input samples to be used for machine learning model </dd> </dl> ``y_train`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples) <br/> <dl> <dd> The target values (class labels in classification, real numbers in regression). </dd> </dl> ``X_valid`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/> <dl> <dd> Validation input samples </dd> </dl> ``y_valid`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples)  <br/> <dl> <dd> The Validation target values . </dd> </dl> ``verbose`` : bool,default=True  <br/> <dl> <dd> Print results for iterations </dd> </dl>| 
| Returns  | ``best_feature_list `` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### plot_history()
Plot results across iterations

#### Example 
```python
from sklearn.metrics import log_loss
# define your own objective function, make sure the function receives four parameters,
#  fit your model and return the objective value ! 
def objective_function_topass(model,X_train, y_train, X_valid, y_valid):      
    model.fit(X_train,y_train)  
    P=log_loss(y_valid,model.predict_proba(X_valid))
    return P
    
# import an algorithm !  
from zoofs import GeneticOptimization
# create object of algorithm
algo_object=GeneticOptimization(objective_function_topass,n_iteration=20,
                            population_size=20,selective_pressure=2,elitism=2,
                            mutation_rate=0.05,minimize=True)
import lightgbm as lgb
lgb_model = lgb.LGBMClassifier()                            
# fit the algorithm
algo_object.fit(lgb_model,X_train, y_train,X_valid, y_valid, verbose=True)
#plot your results
algo_object.plot_history()
```  
### _Gravitational Algorithm_
![Gravitational Algorithm](https://media.giphy.com/media/d1zp7XeNrzpWo/giphy.gif)

------------------------------------------
#### class zoofs.GravitationalOptimization(self,objective_function,n_iteration=50,population_size=50,g0=100,eps=0.5,minimize=True)
------------------------------------------
|  |  |
|----------|-------------|
|  Parameters  | ``objective_function`` :  user made function of the signature 'func(model,X_train,y_train,X_test,y_test)'. <br/> <dl> <dd> The function must return a value, that needs to be minimized/maximized. </dd> </dl> ``n_iteration``: int, default=50 <br/> <dl> <dd> Number of time the algorithm will run  </dd> </dl> ``population_size`` : int, default=50 <br/> <dl> <dd> Total size of the population  </dd> </dl> ``g0``: float, default=100 <br/> <dl> <dd> gravitational strength constant </dd> </dl> ``eps``: float, default=0.5 <br/> <dl> <dd> distance constant </dd> </dl>``minimize``: bool, default=True <br/> <dl> <dd> Defines if the objective value is to be maximized or minimized </dd> </dl>| 
| Attributes | ``best_feature_list`` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### Methods

| Methods | Class Name |
|----------|-------------|
|  fit  | Run the algorithm  | 
| plot_history | Plot results achieved across iteration |

#### fit(model,X_train,y_train,X_valid,y_valid,verbose=True)

|  |  |
|----------|-------------|
|   Parameters | ``model`` : <br/> <dl> <dd> machine learning model's object </dd> </dl> ``X_train`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/><dl> <dd> Training input samples to be used for machine learning model </dd> </dl> ``y_train`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples) <br/> <dl> <dd> The target values (class labels in classification, real numbers in regression). </dd> </dl> ``X_valid`` : pandas.core.frame.DataFrame of shape (n_samples, n_features)  <br/> <dl> <dd> Validation input samples </dd> </dl> ``y_valid`` : pandas.core.frame.DataFrame or pandas.core.series.Series of shape (n_samples)  <br/> <dl> <dd> The Validation target values . </dd> </dl> ``verbose`` : bool,default=True  <br/> <dl> <dd> Print results for iterations </dd> </dl>| 
| Returns  | ``best_feature_list `` :  array-like <br/> <dl> <dd> Final best set of features  </dd> </dl> |

#### plot_history()
Plot results across iterations

#### Example 
```python
from sklearn.metrics import log_loss
# define your own objective function, make sure the function receives four parameters,
#  fit your model and return the objective value ! 
def objective_function_topass(model,X_train, y_train, X_valid, y_valid):      
    model.fit(X_train,y_train)  
    P=log_loss(y_valid,model.predict_proba(X_valid))
    return P
    
# import an algorithm !  
from zoofs import GravitationalOptimization
# create object of algorithm
algo_object=GravitationalOptimization(objective_function,n_iteration=50,
                                population_size=50,g0=100,eps=0.5,minimize=True) 
import lightgbm as lgb
lgb_model = lgb.LGBMClassifier()                                
# fit the algorithm
algo_object.fit(lgb_model,X_train, y_train, X_valid, y_valid, verbose=True)
#plot your results
algo_object.plot_history()
```  

----------------------------

## Support `zoofs`

The development of ``zoofs`` relies completely on contributions.

#### Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## First roll out 
*, 2021 *

## License
[apache-2.0](https://choosealicense.com/licenses/apache-2.0/)
