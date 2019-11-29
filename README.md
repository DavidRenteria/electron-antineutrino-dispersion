# Particle physics phenomenology with Python 3: electron-antineutrino to electron-antineutrino scattering in the Fermi theory
These codes in Python 3 are used to calculate the scattering cross section of electron-antineutrino process. The file
`Montecarlo`  is a pseudocode written in Python 3 to make the computation of the Cross Section by means of the Montecarlo method, while, the file `Riemann sums` makes the calculation of the same Cross Section by means of the Riemann sums method. Meanwhile, the file `Invariant amplitude` is a function, also written in Python 3, used by both methods and it corresponds to the calculation of the squared modulus of the invariant amplitude of scattering for the electron-antineutrino process. Finally, in the `Modules` 
folder, we find the pseudocodes `Differential cross section`, `RGE's` and `Invariant amplitude`  which are used to compute and plot the differential cross section, to solve the renormalization group equations and to obtain the matrix element of the process, respectively. These last files are employed by the Monte Carlo method and Riemann sums.
## Review
The general idea is compute the equation (30) numerically through the generation of random momenta in the x, y and z components with a center of mass energy lower than 1 TeV. In this way, we build a set of random four vectors for the electron and antineutrino with angles between 0 and 180 degrees.

It is known that the Fermi constant depends on the coupling constant, as it is written equation (15), this means that the Fermi constant varies with respect to energy. In order to compute its value for a particular center of mass energy, we solve the group renormalization equations (file `RGE's` ) the first step is to solve the equation (17), in order to know *G_F* at the energy scale. The method used to solve the system of differential equations in Phyton is Runge-Kutta 4.

The next step consists in computing the `Invariant amplitude`  with the help of equation (31). But to program the equation (31), we have code the *gamma* matrices of equation (9) and *gamma_5* as shown in table 2.

Once the *gamma_i* and *gamma_5* matrices have been computed, we create a function to calculate the invariant amplitude averaged over spins. Therefore, we are now able to calculate the cross section distribution.

In order to compute the differential cross section (file `Differential cross 
section`), we generate events for energy processes from 0 GeV to 1000 GeV and we computed the Fermi constant  *G_F* to the energy of the event. The events have been conditioned in order to fulfill momentum conservation. Equation (30) has not been computed directly with Python 3, but with the help of equation (34) instead.


## Montecarlo

Finally to obtain the distribution, we will have to make an adjustment with *curve_fit* on the enveloping points of the dispersion obtained and plot for energies less than 1000 GeV. To compute the total cross section with the Monte Carlo method we have used the *curve_fit* adjustment and then we used the Monte Carlo method to calculate the area of the fit.


```disAleatoriaX=[]
disAleatoriaY=[] 
disBajoLaCurvaX=[]
disBajoLaCurvaY=[]
interaction = 50000
for i in range (interaction):
    x=180*random.random()
    y=max(SEpRegresion+0.01)*random.random()
    if y<=regresion(x):
        disBajoLaCurvaX.append(x)
        disBajoLaCurvaY.append(y)
    else:
        disAleatoriaX.append(x)
        disAleatoriaY.append(y)


areaMontecarlo=((len(disBajoLaCurvaY))/(len(disBajoLaCurvaY)+len(disAleatoriaY)))*(180*max(SEpRegresion+0.01))*(pi/180)
areaMontecarlo
```


## Riemman sums
While with Riemann sums, instead of making an adjustment  we have sum the areas generated by points of the envelope in 50 equal intervals. 

```areaBajoLaCurva=0
for i in range(len(nuevoAng)-1):
    areaBajoLaCurva=areaBajoLaCurva+(vecindad*pi/180)*nuevoSEp[i+1]
areaBajoLaCurva
```


