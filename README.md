# 25.Abril.16
###METODOS SENCILLOS DE PRONÓSTICOS
###Método  de la Media
###En este metodo las proyecciones de los valores futuros son iguales a la media de os datos históricos
###meanf(st,h)... st es la serie de tiempo y h es el numero de periodos a pronosticar

### Ingenuo
###Las previsiones se fijan por el valor de la ultima observacion.
###naive (st,h)

###Ingenuo estacional
###Se pronostica con le mismo valor del mismo periodo del año
###snaive(st,h)

###Deriva
###Permite que las proyecciones puedan aumentar o disminuir con el tiempo
###rwf(y,h,drift=TRUE)
install.packages("fpp")
library (fpp)
labo <- read.csv ("C:\\Users\\SALA-C13\\Downloads\\indicadores_laborales.csv")
part <- ts (labo[,1],start =2005, frequency = 4)
plot (part)
Acf (part)

#######Metodo de la media###########
meanf(part)
partpro <- meanf(part,4)
plot(partpro)
deso <- ts(labo [,1], start  = 2005, frequency = 4)
plot (deso)
Acf (deso)
### part es la ST 
### el número de datos a proyectar en este caso elegí h = 3

########## ingenuo###############
partnai <- naive(part, 4)
plot (partnai)
rwf(part, 3) # Alternativo

### ingenuo estacional
partsnai <- snaive(part, 4)
partsnai
plot(partsnai)
help (snaive)

########## metodo de la deriva
partder <- rwf(part, 4, drift = T)
partder
plot (partder)
#rwf(st, h, drift=TRUE)

############# EJEMPLOS######################33
part1 <- window(part,start=2005,end=2010)
partaj1 <- meanf(part1, h=4)
partaj2 <- naive(part1, h=4)
partaj3 <- snaive(part1, h=4)

plot(part, plot.conf=FALSE, xlim = c(2005, 2011),
    main="Proyección tasas de desempleo trimestre")
lines(partaj1$mean,col=1)
lines(partaj2$mean,col=2)
lines(partaj3$mean,col=3)
legend("topleft",lty=1,col=c(1,2,3,4),
       legend=c("metodo media","metodo ingenuo","metodo ingenuo estacional"))
###Tarea: tasa de crecimiento del pib hasta el 2015 anual
