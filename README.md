# Multiscale-Spectral-Method-Capillarity
Spectral-Method-Capillarity
Spectral methods for capillary surfaces

GPL-3.0-or-later

As of June 8th, 2023, two prototype problems have been treated, with corresponding codes.

Each of these programs needs Chebfun. Please install Chebfun from chebfun.org.

P1
symmetric_capillary_disc_3z.m

This code solves for capillary surfaces that are the image of a disk. The inputs are the radius b, the inlination angle psi_b there, and d, which is a parameter used to create 3 subdomains and offsets from b towards the center. 
We require -\pi \leq\psi_b\leq\pi. The output is the surface.

P2
These codes solve for capillary surfaces that are the image of an annulus. The inputs are the radii a and b with 0<a<b<\infty, the inlination angles \psi_a and \psi_b there, and d, a parameter used to create subdomains and offsets from a and b towards the center. The third solver in this category employs an additional parameter, psi_c, used to separate the leftmost domain into two additional subdomains for cases when |psi_a| > pi/2 . The default for this parameter is psi_c = -pi/2.
We require -\pi \leq\psi_a,\psi_b\leq\pi. The output is the surface.

symmetric_capillary_annular_3z.m

This code solves for capillary surfaces that are the image of an annulus by dividing the original domain into three distinct radial subdomains. It is most effective in cases where a << inf and b is moderately sized. It suffers when the gap between a and b is small. The parameter d is chosen based upon the distance between a and b. As a general rule, the default value for d has been chosen to be the closest integer value to (b-a)/10.

symmetric_capillary_annular_2z.m

This code solves for capillary surfaces that are the image of an annulus by dividing the original domain into two distinct radial subdomains after using an interpolation function to generate an initial guess. It is most effective in cases where a << 1 and b is small. It suffers when |psi_a| is close to -pi. The parameter d is chosen based upon the distance between a and b. The default for this parameter is d = 0.2. 

symmetric_capillary_annular_2z_to_3z.m

This code solves for capillary surfaces that are the image of an annulus by dividing the original domain into two distinct radial subdomains after using an interpolation function to generate an initial guess. The leftmost subdomain is then partitioned into two new, distinct angular subdomains. It is most effective in cases where a << 1 and b is small. It is an improvement upon the strictly two-subdomain code above, but still suffers when |psi_a| is close to -pi.

Interpolation Function
symmetric_capillary_annular_interpolation_func.m

This file is used in the two-subdomain solvers for capillary surfaces that are the image of an annulus. It is used to generate the intial guess in each of those two codes. The codes symmetric_capillary_annular_2z.m and symmetric_capillary_annular_2z_to_3z.m depend on this interpolation function and will not run without it.


Comments
These codes are designed for challenging problems where the base codes have trouble. As such, the codes provided may need modification in order to run properly.

For modest problems, the convergence to solutions is extremely fast and uses very little memory.

For more challenging problems the adaptive algorithm automatically increases the number of Chebyshev points to achieve the prescribed tolerances. This process has worked very well in almost all of the cases we have found.

It is possible sometimes to break these codes for extremes of the inclination angles near +/- pi and either radii too close to each other with \psi_a\psi_b > 0, inner radius a too close to 0, b too large, or the radii too far apart . Typically this happens when |\psi_a|, |\psi_b| > \pi/2, and the closer to \pm\pi, the more challenging. For these multi-scale problems customizing the initial guess and carefully tuning the increase of the Chebyshev nodes inside the adaptive part of the algorithm can lead to success when the base code does not converge. Still, some rather extreme problems may not work even then, and for those problems a multi-scale approach is needed. This is the subject of a future paper.
