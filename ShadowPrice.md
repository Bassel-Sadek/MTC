[[Home]] > [[TravelModel]] > [[UsersGuide]] > [[DataDictionary]] > [[ShadowPrice]]

---

The mandatory destination choice models limit the number of workers (or students) who work (or attend school) in a given location via shadow pricing. For example, consider a travel analysis zone, label it X, in which 50 people work (i.e. the zone's employment is 50). In the first pass of the destination choice model, 200 workers choose zone X has their workplace location. Because zone X is oversubscribed, an additional disutility (or shadow price) is applied to zone X and the destination choice model is executed again. This process continues, per the user's preference, with a goal of limiting the number of workers who work in each zone to the employment of each zone. Mechanically, the "size" terms for each destination are scaled by the total origins to determine the maximum number of travelers allowed in each sub-zone.

The table below defines each of the columns in the shadow pricing output files. Note that the below columns are written for the following trip purposes (substitute these names for &lt;purpose&gt;): work_low, work_med, work_high, work_very_high, university, school_high, school_grade.

| Name | Definition |
|------|------------|
| alt | A unique identifier of the alternative considered in the destination choice model. The alternative is a unique zone/sub-zone combination. |
| zone | The travel analysis zone of the alternative |
| sub-zone | The walk-to-transit destination sub-zone |
| &lt;purpose&gt;_origins | Tours generated at this zone/sub-zone |
| &lt;purpose&gt;_sizeOriginal | Size term, which is specified in the UtilityExpressionCalculator, for each destination alternative |
| &lt;purpose&gt;_sizeAdjOriginal | Shadow pricing routine allows the user to intervene by manually adjusting size terms -- not implemented in our travel model |
| &lt;purpose&gt;_sizeScaled | Size term scaled ... |
| &lt;purpose&gt;_sizePrevious | Size term from the previous iteration of shadow pricing |
| &lt;purpose&gt;_modeledDests | Number of simulated destinations for each alternative (sum should equal sum of origins) |
| &lt;purpose&gt;_sizeFinal | Size term to be used for the next iteration of shadow pricing |
| &lt;purpose&gt;_shadowPrices | Shadow price for the alternative, which is !sizePrevious divided by !modeledDests |
 

-- Main.DavidOry - 25 Jul 2012