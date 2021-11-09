# Entity types

Here is the list of possible types that can be returned by [named entity recognition](../../guide/entity-recognition/index.md) and [relation extraction](../../guide/relation-extraction/index.md).

Uppercase labels are used for named entities. If the label is lowercase, and this can be given in the attributes of named entities or in the elements related to the verb in a relation, it means it is a generic entity.

For example, in the text

    Felipe is a florist.

_florist_ can be labeled `nph` because a florist is a person, but not a specific one.  
_Felipe_, on the other hand, is a specific person identified by a proper name, so he is labeled with `NPH`.

Label | Description | Example
--- | --- | ---
`ADR` | Street address | Who lived at **221B Baker Street**?
`ANM` | Animal | **Felix** is an anthropomorphic black cat.
`BLD` | Building | While in London I attended a concert at the **Royal Albert Hall**.
`COM` | Company, business | **Tesla Inc.** sold 10% of its Bitcoin holdings.
`DAT` | Date | Napoleon died on **May 5, 1821**.
`DEV` | Device | My new **Galaxy** smartphone has seven cameras.
`DOC` | Document | I appeal to the **Geneva Convention**!
`EVN` | Event | Eddy Merckx won the **Tour de France** five times..
`FDD` | Food, beverage | Frank likes to drink **Guinness** beer.
`GEA` | Physical geographic feature | I crossed the **Mississipi** river with my boat
`GEO` | Administrative geographic area | **Alaska** is the least densely populated state in the **United States**.
`GEX` | Extended geography | The astronauts have landed on **Mars**.
`HOU` | Hours | The eclipse reached its peak at **3pm**.
`LEN` | Legal entity | Of course I pay the **FICA** tax.
`MAI` | Email address | For any questions do not hesitate to write to **helpme@somedomain.com**.
`MEA` | Measure | The chest is **five feet** wide and **40 inches** tall.
`MMD` | Mass media | I read it in the **Guardian**.
`MON` | Money | I sold half of my stock and made **six hundred thousand dollars**.
`NPH` | Person | **Hakeem Olajuwon** dunked effortlessly.
`NPR` | Unrecognized entity with a proper noun | I like **GYYYJJJ7** soooo much!
`ORG` | Organization, institution, society | Now they threaten to quit the **United Nations** if they are not heard.
`PCT` | Percentage | The richest **10%** of adults in the world own **85%** of global wealth.
`PHO` | Phone number | For poor database design, call **(214) 748-3647**.
`PPH` | Physical phenomena | The **COVID-19** infection is slowing down.
`PRD` | Product | The **Rolex Daytona** is an wonderful watch.
`VCL` | Vehicle | A **Ferrari 250 GTO** was the most expensive car ever sold.
`WEB` | Web address | Find the best technical documentation at **docs.expert.ai**.
`WRK` | Work of human intelligence | **Grease** is a funny  musical romantic comedy.
