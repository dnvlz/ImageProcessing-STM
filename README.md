# ImageProcessing-STM
## 3D plotting of the surface of the Earth and of scanning tunneling microscope measurements of a silicon surface.


When light strikes a surface, the amount falling per unit area depends
not only on the intensity of the light, but also on the angle of
incidence. If the light makes an angle *θ* to the normal, it only “sees”
cos *θ* of area per unit of actual area on the surface:

So the intensity of illumination is *a*cos *θ*, if *a* is the raw
intensity of the light. This simple physical law is a central element of
3D computer graphics. It allows us to calculate how light falls on
three-dimensional objects and hence how they will look when illuminated
from various angles.

Suppose, for instance, that we are looking down on the Earth from above
and we see mountains. We know the height of the mountains *w*(*x*,*y*)
as a function of position in the plane, so the equation for the Earth’s
surface is simply *z* = *w*(*x*,*y*), or equivalently
*w*(*x*,*y*) − *z* = 0, and the normal vector *v⃗* to the surface is
given by the gradient of *w*(*x*,*y*) − *z* thus:

$$\vec{v} =
\nabla \[w(x,y)-z\] = \begin{pmatrix}
                  \partial/\partial x \\\\
                  \partial/\partial y \\\\
                  \partial/\partial z
                \end{pmatrix}
                \[w(x,y)-z\]
              = \begin{pmatrix}
                  \partial w/\partial x \\\\
                  \partial w/\partial y \\\\
                  -1
                \end{pmatrix}.$$
                
Now suppose we have light coming in represented by a vector *a⃗* with
magnitude equal to the intensity of the light. Then the dot product of
the vectors *a⃗* and *v⃗* is
*a⃗* ⋅ *v⃗* = \|*a⃗*\| \|*v⃗*\|cos *θ*,
where *θ* is the angle between the vectors. Thus the intensity of
illumination of the surface of the mountains is

$$I = \|\vec{a}\| \cos\theta = {\vec{a}\cdot\vec{v}\over\|\vec{v}\|}
  = {a_x (\partial w/\partial x)
   + a_y (\partial w/\partial y) - a_z\over
     \sqrt{(\partial w/\partial x)^2 + (\partial w/\partial y)^2 + 1}}.$$
     
Let’s take a simple case where the light is shining horizontally with
unit intensity, along a line an angle *ϕ* counter-clockwise from the
east-west axis, so that *a* = (cos*ϕ*,sin*ϕ*,0). Then our intensity of
illumination simplifies to

$$I = {\cos\phi\\,(\partial w/\partial x) + \sin\phi\\,(\partial w/\partial y)\over
     \sqrt{(\partial w/\partial x)^2 + (\partial w/\partial y)^2 + 1}}.$$
     
If we can calculate the derivatives of the height *w*(*x*,*y*) and we
know *ϕ* we can calculate the intensity at any point.

1.  The file `altitude.txt` contains the altitude *w*(*x*,*y*) in meters
    above sea level (or depth below sea level) of the surface of the
    Earth, measured on a grid of points (*x*,*y*). By reading this file
    and storing the data in an array, we can calculate the derivatives
    ∂*w*/∂*x* and ∂*w*/∂*y* at each grid point. To calculate the
    derivatives we need to know the value of *h*, the distance in meters
    between grid points, which is about 30 000 m in this case. (It’s
    actually not precisely constant because we are representing the
    spherical Earth on a flat map, but *h* = 30 000 m will give
    reasonable results.)

2.  Using the values for the derivatives, we compute the intensity for
    each grid point, with *ϕ* = 45<sup>∘</sup>, and make a density plot
    of the resulting values in which the brightness of each dot depends
    on the corresponding intensity value.

    Note that the value of the intensity *I* from the formula above can
    be either positive or negative—it ranges from  + 1 to  − 1. What
    does a negative intensity mean? It means that the area in question
    is *in shadow*—it lies on the wrong side of the mountain to receive
    any light at all.

3.  The file `stm.txt` contains a grid of values from scanning tunneling
    microscope measurements of the (111) surface of silicon. A scanning
    tunneling microscope (STM) is a device that measures the shape of
    surfaces at the atomic level by tracking a sharp tip over the
    surface and measuring quantum tunneling current as a function of
    position. The end result is a grid of values that represent the
    height of the surface as a function of position and the data in the
    file `stm.txt` contain just such a grid of values. By modifying the
    previous program, we can also visualize the STM data and hence
    create a 3D picture of what the silicon surface looks like. The
    value of *h* for the derivatives in this case is around *h* = 2.5
    (in arbitrary units).
