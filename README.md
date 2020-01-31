# Particle physics phenomenology with Python 3: electron-antineutrino to electron-antineutrino scattering in the Fermi theory
These codes in Python 3 are used to calculate the scattering cross section of electron-antineutrino process. The file
`Montecarlo`  is a pseudocode written in Python 3 to make the computation of the Cross Section by means of the Montecarlo method, while, the file `Riemann sums` makes the calculation of the same Cross Section by means of the Riemann sums method. The *invariant amplitude* is a function, also written in Python 3, used by both methods and it corresponds to the calculation of the squared modulus of the invariant amplitude of scattering for the electron-antineutrino process. Finally, the pseudocodes *differential cross section*, *RGE's* and *invariant amplitude*  which are used within the `Montecarlo` and `Riemann sums` files to calculate the differential cross section.
## Review
The general idea is compute the equation (19) numerically through the generation of random momenta in the x, y and z components with a center of mass energy lower than 1 TeV. In this way, we build a set of random four vectors for the electron and antineutrino with angles between 0 and 180 degrees.

It is known that the Fermi constant depends on the coupling constant, as it is written equation (12), this means that the Fermi constant varies with respect to energy. In order to compute its value for a particular center of mass energy, we solve the group renormalization equations (RGE's), this is an extra exercise we have done to adapt the *G_F* to the energy in the center of mass ,in order to know *G_F* at the energy scale. The method used to solve the system of differential equations in Phyton is Runge-Kutta 4.

The next step consists in computing the `Invariant amplitude`  with the help of equation (20). But to program the equation (20), we have code the *gamma* matrices of equation (9) and *gamma_5* as shown in table 2.

Once the *gamma_i* and *gamma_5* matrices have been computed, we create a function to calculate the invariant amplitude averaged over spins. Therefore, we are now able to calculate the cross section distribution.

In order to compute the differential cross section (file `Differential cross 
section`), we generate events for energy processes from 0 GeV to 1000 GeV and we computed the Fermi constant  *G_F* to the energy of the event. The events have been conditioned in order to fulfill momentum conservation. Equation (19) has not been computed directly with Python 3, but with the help of equation (23) instead.


## Montecarlo

Finally to obtain the distribution, we will have to make an adjustment with *curve_fit* on the enveloping points of the dispersion obtained and plot for energies less than 1000 GeV. To compute the total cross section with the Monte Carlo method we have used the *curve_fit* adjustment and then we used the Monte Carlo method to calculate the area of the fit.


```dispertion_randomX=[]
dispertion_randomY=[] 
dispertion_BelowCurveX=[]
dispertion_BelowCurveY=[]
interaction = 50000
for i in range (interaction):
    x=180*random.random()
    y=max(SEpRegression+0.01)*random.random()
    if y<=regression(x):
        dispertion_BelowCurveX.append(x)
        dispertion_BelowCurveY.append(y)

    else:
        dispertion_randomX.append(x)
        dispertion_randomY.append(y)


areaMontecarlo=((len(dispertion_BelowCurveY))/(len(dispertion_BelowCurveY)+len(dispertion_randomY)))*(180*max(SEpRegression+0.01))*(pi/180)
areaMontecarlo #total cross section
```


## Riemman sums
While with Riemann sums, instead of making an adjustment  we have sum the areas generated by points of the envelope in 50 equal intervals. 

```area_Riemann_sums=0
for i in range(len(newAng)-1):
    area_Riemann_sums=area_Riemann_sums+(gap*pi/180)*newSEp[i+1]
area_Riemann_sums #total cross section
```


