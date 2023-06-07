# Buffering 

Buffering is a useful procedure when you want to be able to define distances from features. These can be:
-   Rings around point features (you can have multiple rings)
-   Buffers around line features
-   Buffers around polygon boundaries (inside or outside the polygons) 

Distance can be constant or variable, that is, based on an attribute value.

# Overlay Analysis

**Union**
- Considered an "OR" operator
- All information from BOTH layers is included

**Intersect**
- Considered an "AND" operator
- Only space that is shared between the two features is included
---
Example I - Buffer around line feature:

<img width="884" alt="Screen Shot 2023-06-07 at 3 22 45 PM" src="https://github.com/RutaCodes/GeoSpatial/assets/111301407/d8441331-5182-40a5-88e3-b5848e74e2ae">

---
Example II - Buffer around point features:

<img width="883" alt="Screen Shot 2023-06-07 at 3 29 17 PM" src="https://github.com/RutaCodes/GeoSpatial/assets/111301407/6ac43fa1-fd74-4d00-bd65-6e24b336798b">

---
Example III - Buffer, Intersect and Erase:

<img width="887" alt="Screen Shot 2023-06-07 at 3 25 41 PM" src="https://github.com/RutaCodes/GeoSpatial/assets/111301407/a0c6493c-4980-4994-9188-429c4763899d">

All the parcels that are outside of a 1000 foot municipality buffer.

---
Example IV - Buffers and Intersect:

<img width="885" alt="Screen Shot 2023-06-07 at 3 14 19 PM" src="https://github.com/RutaCodes/GeoSpatial/assets/111301407/cdc6e067-9b85-4634-bbd4-bb3bd219f2f7">

1) "Drug-free zone" (1000m) buffer around the school base was created
2) To see how many parcels were affected by this buffer, an intersect of the school buffer layer with the parcels layer was done
3) Then we are able to highlight how many of those parcels are classified as bars or restaurants
