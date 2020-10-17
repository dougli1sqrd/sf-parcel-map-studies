Land use categories for every parcel in San Francisco. The land use categories are derived from a range of City and commercial databases. Where building square footages were missing from these databases they were derived from a LIDAR survey flown in 2007.

Land use categories are as follows (units are square feet):
CIE = Cultural, Institutional, Educational
MED = Medical
MIPS = Office (Management, Information, Professional Services)
MIXED = Mixed Uses (Without Residential)
MIXRES = Mixed Uses (With Residential)
PDR = Industrial (Production, Distribution, Repair)
RETAIL/ENT = Retail, Entertainment
RESIDENT = Residential
VISITOR = Hotels, Visitor Services
VACANT = Vacant
ROW = Right-of-Way
OPENSPACE = Open Space

Other attributes are:
RESUNITS = Residential Units
BLDGSQFT = Square footage data
YRBUILT = year built
TOTAL_USES = Business points from Dun & Bradstreet were spatially aggregated to the closest parcel, and this field is the sum of the square footage fields
The subsequent fields (CIE, MED, MIPS, RETAIL, PDER & VISITOR) were derived using the NAICS codes supplied in the Dun & Bradstreet dataset, and the previous TOTAL_USES column.

The determining factor for a parcel's LANDUSE is if the square footage of any non-residential use is 80% or more of its total uses. Otherwise it becomes MIXED.

In the case where RESIDENT use has some square footage of non-residential use, this is mainly accessory uses such as home businesses, freelancers, etc.
Last updated: March, 2016
