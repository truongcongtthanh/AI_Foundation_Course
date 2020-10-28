# Genetic Algorithm
## Introduction
![](https://i.imgur.com/RRwYSOM.png)
Genetic is a Algorithm, which from a inital Population 
We will evaluate gens in this population
and then, we will put these gen in order
We will select randomly some gens 
Then, we will change it by Crossover And Mutation to create gens which better
Repeat the above processes until found best gen

![](https://i.imgur.com/PJqPF8O.png)
inital Population

![](https://i.imgur.com/rSP7Z7N.png)
Evaluation

![](https://i.imgur.com/q201iuI.png)
![](https://i.imgur.com/1cNcMUb.png)
Selection

![](https://i.imgur.com/fkBaG25.png)
Crossover

![](https://i.imgur.com/5CAG1RC.png)
Mutation

## some applications
### 1. find the min of a function
![](https://i.imgur.com/Yqupt9s.png)
![](https://i.imgur.com/aYaq6yN.png)
```python=
import random

size_of_individual = 5
size_of_population = 100
n_generations = 100


losses = []

def generate_random_value(bound = 10):
    return (random.random()*2 - 1)*bound

def score_fitness(individual): # cost
    return sum(val*val for val in individual)

def create_individual():
    return [generate_random_value() for _ in range(size_of_individual)]

def crossover(individual1, individual2, crossover_rate = 0.9):
    individual1_new = individual1.copy()
    individual2_new = individual2.copy()
    
    for i in range(size_of_individual):
        if random.random() < crossover_rate:
            individual1_new[i] = individual2[i]
            individual2_new[i] = individual1[i]
            
    
    return individual1_new, individual2_new

def mutate(individual, mutation_rate = 0.05):
    individual_m = individual.copy()
    
    for i in range(size_of_individual):
        if random.random() < mutation_rate:
            individual_m[i] = generate_random_value()
        
    return individual_m

def selection(sorted_old_population):
    
    index1 = random.randint(0, size_of_population-1)    
    while True:
        index2 = random.randint(0, size_of_population-1)    
        if (index2 != index1):
            break
            
    individual_s = sorted_old_population[index1]
    if index2 < index1:
        individual_s = sorted_old_population[index2]
    
    return individual_s 

def create_new_population(old_population, elitism=0, gen=1):
    sorted_population = sorted(old_population,key=score_fitness)
        
    if gen%1 == 0:
        losses.append(score_fitness(sorted_population[0]))
        print("BEST:", score_fitness(sorted_population[0]))
    
    new_population = sorted_population[:elitism]   
    
    while len(new_population) < size_of_population:
        # selection
        individual_s1 = selection(sorted_population)
        individual_s2 = selection(sorted_population) # duplication
        
        # crossover
        individual_c1, individual_c2 = crossover(individual_s1, individual_s2)
        
        # mutation
        individual_m1 = mutate(individual_c1)
        individual_m2 = mutate(individual_c2)
        
        new_population.append(individual_m1)
        new_population.append(individual_m2)
            
    return new_population


population = [create_individual() for _ in range(size_of_population)]

for i in range(n_generations):
    population = create_new_population(population, 2, i)
```

## 2. House price prediction
![](https://i.imgur.com/kStEasq.png)
![](https://i.imgur.com/RPv7oZa.png)

```python=
# aivietnam.ai - estimation of house prices
import random

n = 2                  # size of individual (chromosome)
m = 100                # size of population
n_generations = 2000   # number of generations
losses = []            # để vẽ biểu đồ quá trình tối ưu

# Hàm load data
def load_data():
    # kết nối với file
    file = open('data.csv','r')

    # readlines giúp việc đọc file theo từng dòng , mỗi dòng là 1 chuỗi
    lines = file.readlines()
    
    areas  = []
    prices = []
    for i in range(10): 
        string = lines[i].split(',')
        areas.append(float(string[0]))
        prices.append(float(string[1]))

    # Đóng kết nối với file
    file.close()
    
    return areas, prices

# load data
areas, prices = load_data()

def generate_random_value(bound = 200):
    return (random.random()-0.5)*bound

def compute_loss(individual):
    result = 65534
    
    a = individual[0]
    b = individual[1]    
    estimated_prices = [a*x + b for x in areas]
    
    # all prices should be positive numbers
    num_negetive_prices = sum(p < 0 for p in estimated_prices)
    if num_negetive_prices == 0:        
        losses = [abs(y_est-y_gt) for y_est, y_gt in zip(estimated_prices, prices)]
        result = sum(losses)
    
    return result

def compute_fitness(individual):
    loss = compute_loss(individual)
    fitness = 1 / (loss + 1)
    return fitness

def create_individual():
    return [generate_random_value() for _ in range(n)]

def crossover(individual1, individual2, crossover_rate = 0.9):
    individual1_new = individual1.copy()
    individual2_new = individual2.copy()
    
    for i in range(n):
        if random.random() < crossover_rate:
            individual1_new[i] = individual2[i]
            individual2_new[i] = individual1[i]            
    
    return individual1_new, individual2_new

def mutate(individual, mutation_rate = 0.05):
    individual_m = individual.copy()
    
    for i in range(n):
        if random.random() < mutation_rate:
            individual_m[i] = generate_random_value()
        
    return individual_m

def selection(sorted_old_population):    
    index1 = random.randint(0, m-1)    
    while True:
        index2 = random.randint(0, m-1)    
        if (index2 != index1):
            break
            
    individual_s = sorted_old_population[index1]
    if index2 > index1:
        individual_s = sorted_old_population[index2]
    
    return individual_s 

def create_new_population(old_population, elitism=2, gen=1):
    sorted_population = sorted(old_population, key=compute_fitness)
        
    if gen%1 == 0:
        losses.append(compute_loss(sorted_population[m-1]))
        #print("Best loss:", compute_loss(sorted_population[m-1]), sorted_population[m-1])      
    
    new_population = []
    while len(new_population) < m-elitism:
        # selection
        individual_s1 = selection(sorted_population)
        individual_s2 = selection(sorted_population) # duplication
        
        # crossover
        individual_c1, individual_c2 = crossover(individual_s1, individual_s2)
        
        # mutation
        individual_m1 = mutate(individual_c1)
        individual_m2 = mutate(individual_c2)
        
        new_population.append(individual_m1)
        new_population.append(individual_m2)            
    
    for ind in sorted_population[m-elitism:]:
        new_population.append(ind.copy())
    
    return new_population

population = [create_individual() for _ in range(m)]
for i in range(n_generations):
    population = create_new_population(population, 2, i)
```
<p align="right">Slide and source code from Dinh Quang Vinh teacher<p align="right">
