Airfoils
------------

windIO describes the airfoils in terms of coordinates and polars. The yaml entry airfoils consists of a list of elements. Each is characterized by the following fields:

   -  :code:`name`
   -  :code:`coordinates`
   -  :code:`relative_thickness`
   -  :code:`aerodynamic_center`
   -  :code:`polars`

The airfoils listed in this database are not all necessarily used in the blade. Only the ones called in :code:`airfoil_position' within :code:`outer_shape_bem` will actually be loaded to model the blade.

**name**
:code:`name` is a plain string identifying the airfoils

**coordinates**
The airfoil coordinates are specified here in the sub-fields :code:`x` and :code:`y`. :code:`x` and :code:`y` must have the same length. :code:`x` must be defined between 0, which corresponds to the leading edge, and 1, which corresponds to the trailing edge. Airfoil coordinates should be defined from trailing edge (:code:`x=1`) towards the suction side (mostly positive :code:`y` values), to leading edge (:code:`x=0`, :code:`y=0`), to the pressure side (mostly negative :code:`y`), and conclude at the trailing edge pressure side (:code:`x=1`). Flatback airfoils can be defined either open (:code:`x=1`, :code:`y!=0`) or closed (:code:`x=1`, :code:`y=0`).

**relative_thickness**
Float defined between 0 (plate) and 1 (cylinder) to specify the relative thickness of the airfoil. This generates a small redundancy (it could be determined from the field coordinates), but it simplifies the converters.

**aerodynamic_center**
Float defined between 0 (leading edge) and 1 (trailing edge) to specify the chordwise coordinate of the aerodynamic center used to define the polars.

**polars**
List of sets of polars. Each entry is marked with a dash (-) mark and must include the following fields

 - :code:`configuration`: plain string to describe and identify the set of polars
 - :code:`re`: Reynolds number of the polars
 - :code:`c_l`: lift coefficient as a function of angle of attack
 - :code:`c_d`: drag coefficient as a function of angle of attack
 - :code:`c_m`: moment coefficient as a function of angle of attack

:code:`c_l`, :code:`c_d`, and :code:`c_m` are defined via arrays :code:`grid` and :code:`values`, which must have the same length. :code:`grid` contains the angles of attack in radians and must be specified between -pi (-3.141592653589793) and pi (+3.141592653589793), while :code:`values` contains the coefficients.