# Modelling between Predators and Preys in Various Population Densities
Final Project MA2151 Simulation and Computational Mathematics

Our purpose this project is to identifying the effect of various population densities on predator performance in hunting prey and comparing simulations between predators and prey with cellular automata techniques and agent-based model techniques.

In the first simulation, namely using the cellular automata (CA) technique, there are 3 numerical descriptions. After being carried out five times with variations in population density, the average iteration for 22 iterations was obtained, and the average remaining prey population was 28.2. The probability of the population density of prey/predators affects the number of remaining prey, where as the population density increases, the number of remaining prey decreases and the percentage of the number of prey will decrease. In the second simulation, namely using the Agent-based model technique, there are 2 numerical descriptions in the initialization of the environment. After being carried out five times with variations in population density, the average iteration for 29 iterations was obtained, and the average remaining prey population was 25.2. As in the cellular automata (CA) method, the probability of the population density of prey/predators affects the number of remaining prey, where as the population density increases, the number of remaining prey decreases and the percentage of the number of prey will decrease. When comparing the two methods, the agent-based model has a longer time than the cellular automata with a difference of 7 iterations, while the cellular automata method has a larger number of prey populations than the agent-based model method with a difference of 3 more prey, but the number of prey and the percentage in both methods have a downward trend when the population probability density increases.

### Library Used :
```
from pickle import TRUE
import random 
import seaborn as sns
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib import colors
import matplotlib
import matplotlib.image as mpimg
import matplotlib.animation as animation
from IPython.display import HTML  # for embedded matplotlib animation
from math import *
```

### Initialization
For Cellular Automata:
```
# Keterangan angka pada matriks lingkungan
EMPTY = 0
PREY = 1
PREDATOR = 2
PREDATOR_ATE = 3

# Fungsi Inisialisasi Matriks Lingkungan dengan status lapar
def initHunger(m = 50, n = 50): #Dibuat ukuran sebesar 50x50 grid
  matHunger = [[0 for i in range(n)] for j in range(m)] #Array matriks lingkungan status lapar
  return matHunger

#Fungsi Inisialisasi Matriks Lingkungan
def initMatrix(probPrey, probPred, matHunger): 
  m = len(matHunger) #Jumlah kolom matriks lingkungan
  n = len(matHunger[0]) #Jumlah baris matriks lingkungan
  mat = [[0 for i in range(n)] for j in range(m)] #Array matriks lingkungan
  for i in range(m):
    for j in range(n):
      rnd = random.random() #Bangkitkan bilangan 0 sampai 1
      if rnd < probPrey: #Mengisi populasi mangsa dengan peluang mangsa dimasukkan
        mat[i][j] = PREY
      elif rnd < probPrey + probPred: #Mengisi populasi predator dengan peluang mangsa dimasukkan
        mat[i][j] = PREDATOR
        matHunger[i][j] = 0 #Atur status lapar pada predator
      else:
        mat[i][j] = EMPTY #Sisanya kosong
  return mat
```

For Agent-Based Modelling
```
# Keterangan angka
EMPTY = 0
PREY = 1
PREDATOR = 2

# Fungsi inisialisasi agen lingkungan
def initAgentMat(agents, probPrey, probPred, m, n): 
  mat = [[0 for i in range(m)] for j in range(n)]

  for i in range(len(mat)):
    for j in range(len(mat[0])):
      rnd = random.random() #Bangkitkan angka 0 sampai 1

      if rnd < probPrey: #Mengisi populasi mangsa dengan peluang mangsa dimasukkan
        agents.append([PREY, i, j, 0]) # Jenis, baris, kolom, status lapar, pada prey diisi 0 dan tidak akan diupdate
      elif rnd < probPrey + probPred: #Mengisi populasi predator dengan peluang predator dimasukkan
        agents.append([PREDATOR, i, j, 0]) # Pada predator status lapar akan diupdate di fungsi lain

  for agent in agents:
    x, y = agent[1], agent[2] #Atur angka 1 dan 2 sebagai posisi x dan y
    mat[x][y] = agent[0] #Atur angka nol sebagai peran

  return mat
```
