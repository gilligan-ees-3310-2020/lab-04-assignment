Lab \#4 Exercises
================
put your name here
Lab: Mon. Feb.\~3 Due: Mon. Feb.\~10.

  - [General Instructions](#general-instructions)
  - [Chapter 5 Exercises](#chapter-5-exercises)
      - [Exercise 5.1: Lapse Rate](#exercise-5.1-lapse-rate)
  - [Chapter 7 Exercises](#chapter-7-exercises)
      - [Exercise 7.2: Clouds and
        Infrared.](#exercise-7.2-clouds-and-infrared.)
      - [Exercise 7.3: Clouds and Visible
        Light.](#exercise-7.3-clouds-and-visible-light.)

# General Instructions

In the past three weeks, we focused on mastering many of the basics of
using R and RMarkdown. For this week’s lab, when you write up the
answers, I would like you to think about integrating your R code chunks
with your text.

For instance, you can describe what you’re going to do to answer the
question, and then for each step, after you describe what you’re going
to do in that step, you can include an R code chunk to do what you just
described, and then the subsequent text can either discuss the results
of what you just did or describe what the next step of the analysis will
do.

This way, your answer can have several small chunks of R code that build
on each other and follow the flow of your text.

# Chapter 5 Exercises

For this model, you will use the RRTM model, which includes both
radiation and convection.

## Exercise 5.1: Lapse Rate

Run the RRTM model in its default configuration and then vary the lapse
rate from 0 to 10 K/km. For each value of the lapse rate, adjust the
surface temperature until the earth loses as much heat as it gains
(i.e., the value of *Q* in the `run_rrtm` model output is zero.)

It will probably be easier to do this with the interactive version of
the RRTM model at <http://climatemodels.uchicago.edu/rrtm/> than with
the R interface `run_rrtm`.

1)  Make a tibble containing the values of the lapse rate and the
    corresponding equilibrium surface temperature, and **make a plot**
    with lapse rate on the horizontal axis and surface temperature on
    the vertical axis.

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer. Integrate the code chunks with your text, so
you explain what you are doing and then present the code that executes
that part of your work.

``` r
# Here is an example of running rrtm_default. 
# Modify it and add additional code to do this exercise.
# 
rrtm_default = run_rrtm(file = "_data/rrtm_default.Rds", T_surface = 284.42,
                        lapse_rate = 6, co2 = 400)
rrtm_default$Q # Energy imbalance: positive means more heat in than out, 
```

    ## [1] 0

``` r
               # negative means more heat out than in.

rrtm_changed = run_rrtm(file = "_data/rrtm_default.Rds", T_surface = 284.42,
                        lapse_rate = 7, co2 = 400)
rrtm_changed$Q # Energy imbalance: positive means more heat in than out, 
```

    ## [1] 1

``` r
               # negative means more heat out than in.
```

For example, you could write: For a lapse rate of 7. K/km, the heat
imbalance is 1.0 W/m<sup>2</sup>. That means that we need to raise the
surface temperature.

Note how I use the R function `ifelse` to automatically choose between
“raise” and “lower” in the text.

2)  Describe how the equilibrium surface temperature varies as the lapse
    rate varies.

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer. Integrate the code chunks with your text, so
you explain what you are doing and then present the code that executes
that part of your work.

``` r
# If you need to, intersperse code chunks in your answer to show your work.
# If you can answer this part without needing R code, you don't need to include
# code chunks.
```

# Chapter 7 Exercises

## Exercise 7.2: Clouds and Infrared.

**Note:** this exercise only considers the effect of clouds on longwave
radiation and ignores the effect of clouds on albedo, which is also
important.

1)  Run the MODTRAN model with present-day CO<sub>2</sub> (400 ppm) and
    a tropical atmosphere. Plot the outgoing infrared spectrum.
    
    Run MODTRAN four times: first with no clouds, and then with three
    different kinds of clouds: standard cirrus, altostratus, and
    stratus. These correspond to high, medium, and low-altitude clouds.
    
    Describe the important differences between the spectra for the four
    cases. Describe the differences in the intensity of outgoing
    infrared radiation \(I_{\text{out}}\) for the four cases.
    
    How do the four spectra compare for the 700 cm<sup>-1</sup> band
    (where CO<sub>2</sub> absorbs strongly) and the 900 cm<sup>-1</sup>
    band (in the atmospheric window)?
    
    Which kind of cloud has the greatest impact on outgoing infrared
    light? Why?

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer.

``` r
# Mix code chunks with your text to show your work
```

2)  Now set `atmosphere` to `"midlatitude winter"`, set `clouds` to
    `"none"`, and set the sensor altitude to 0 km (`altitude_km = 0`)
    and make the sensor look up (`looking = "up"`). This means your
    sensor is on the ground looking up at the longwave radiation coming
    down from the atmosphere to the ground instead of looking down from
    the top of the atmosphere at the longwave radiation going out to
    space.
    
    Run MODTRAN first with `h2o_scale = 1` (the default), and then with
    `h2o_scale = 0` (no water vapor).
    
    Plot the two spectra and compare them. Discuss why you see what you
    see:
    
      - For the atmosphere with no water vapor, compare the parts of the
        spectrum corresponding to the strong CO<sub>2</sub> absorption
        (roughly 600–750 cm<sup>-1</sup>) and the infrared window
        (roughly 800–1200 cm<sup>-1</sup>).
        
          - Which corresponds to higher emission temperatures and which
            to lower temperatures?
          - Why do you think this is?
    
      - For the atmosphere with normal water vapor (`h2o_scale = 1`),
        how does water vapor change the spectrum you see from the
        ground?
        
          - Does it make the longwave radiation brighter (warmer) or
            dimmer (cooler)?
          - Why do you think this is?

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer.

``` r
# Mix code chunks with your text to show your work
```

3)  Keeping the same settings for `atmosphere = "midlatitude winter"`,
    `altitude_km = 0`, and `looking="up"`, set `h2o_scale=1` and run
    MODTRAN first with no clouds, then with three kinds of clouds:
    standard cirrus, altostratus, and stratus (`clouds="none"`,
    `clouds="standard cirrus"`, `clouds="altostratus"`, and
    `clouds="stratus"`).
    
    When we’re looking up at the clouds, the base (bottom) of the clouds
    form a layer that is opaque to longwave radiation, with an
    emissivity of 1 (i.e., a perfect black body).
    
    Cirrus clouds are very high (around 10 km above sea level),
    \`altostratus clouds are at a medium height (with a base around 2.4
    km), and stratus clouds are very low (with a base around 0.33 km).
    
    For each run examine  
    \(I_{\text{down}}\). (Remember that the variable `i_out` in the
    MODTRAN output measures the intensity of longwave radiation reaching
    the sensor. In this exercise, the sensor is on the ground looking
    up, so `i_out` measures the downward radiation reaching the ground.)
    
    Describe how \(I_{\text{down}}\) compares for the four conditions.
    
      - Do the clouds have a heating or cooling effect?
      - Which clouds have the greatest effect?
      - What does this suggest about how clouds affect the ground
        temperature?
    
    As you do this exercise, think about a winter night with clear skies
    versus a winter night with cloudy skies.

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer. Integrate the code chunks with your text, so
you explain what you are doing and then present the code that executes
that part of your work.

``` r
# Mix code chunks with your text to show your work...
```

4)  Plot the longwave radiation spectra for the four MODTRAN runs from
    part (c). Which parts of the spectrum do the different clouds affect
    the most? (Compare the infrared window to the parts of the spectra
    where CO<sub>2</sub> absorbs.)
    
      - Look at two parts of the spectrum: the infrared window (roughly
        800–1200 cm<sup>-1</sup>) and the region where CO<sub>2</sub>
        absorbs strongly (roughly 600–750 cm<sup>-1</sup>).
        
        Why do you suppose the high, medium, and low clouds affect the
        two different spectral regions the way they do?
    
      - In which part of the spectrum do the clouds affect the downward
        longwave radiation the most?

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer.

``` r
# Mix code chunks with your text to show your work
```

## Exercise 7.3: Clouds and Visible Light.

For this exercise, you will use the RRTM model to examine climate
sensitivity and the water vapor feedback in a radiative-convective
atmosphere.

1)  First, run the RRTM model with its default parameters (400 ppm
    CO<sub>2</sub>) and note the surface temperature (`T_surface`).
    
    Then run it again with doubled CO<sub>2</sub> concentration (`co2
    = 800`). Adjust the surface temperature to bring the heat imbalance
    `Q` to zero (it may be easier to do this with the interactive model
    at <http://climatemodels.uchicago.edu/rrtm/> and then paste the new
    surface temperature into your R code).
    
    The change in surface temperature between the 400 ppm CO<sub>2</sub>
    and 800 ppm CO<sub>2</sub> (\(\Delta T_{2 \times \text{CO}_2}\))
    runs is the **climate sensitivity**. What is it?

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer. Integrate the code chunks with your text, so
you explain what you are doing and then present the code that executes
that part of your work.

``` r
# Mix code chunks with your text to show your work...
```

2)  Now run the RRTM model again, for 400 and 800 ppm CO<sub>2</sub>,
    but this time setting `relative_humidity = 0` (this turns off the
    water vapor feedback). At each concentration of CO<sub>2</sub>,
    adjust `T_surface` to bring the heat into balance (so the output has
    `Q` equal to zero). Now what is the climate sensitivity
    (\(\Delta T_{2 \times \text{CO}_2}\))?

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer. Integrate the code chunks with your text, so
you explain what you are doing and then present the code that executes
that part of your work.

``` r
# Mix code chunks with your text to show your work...
```

3)  Compare the climate sensitivity
    (\(\Delta T_{2 \times \text{CO}_2}\)) in part (a) (with water-vapor
    feedback) and part (b) (without water-vapor feedback). The
    amplification factor for the water-vapor feedback is the ratio of
    the climate sensitivity with water-vapor feedback to the sensitivity
    without the feedback. What is it?

**Answer:** *Put your answer here.* Be sure to show your work and
include any data, plots, etc. that you need in order to explain how you
came up with your answer. Integrate the code chunks with your text, so
you explain what you are doing and then present the code that executes
that part of your work.

``` r
# Mix code chunks with your text to show your work...
```
