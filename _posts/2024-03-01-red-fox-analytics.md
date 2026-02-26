## Red Fox Analytics: Rebuilding a Data Company's Infrastructure from the Ground Up

<img src="/assets/images/red-fox-team.jpeg" alt="The Red Fox Analytics team: Matt Mohorn (CTO), Chris Mauzé (CEO), Nathan Koerschner, and Amer Tadmori (COO)" style="width: 100%; max-width: 600px; border-radius: 8px; margin-bottom: 20px;">
<p style="font-size: 0.85em; color: #666; margin-top: -15px; margin-bottom: 30px;">Left to right: Matt Mohorn (CTO), Chris Mauzé (Founder & CEO), myself, and Amer Tadmori (COO)</p>

When I joined Red Fox Analytics in 2022, the company had just crossed $1M in revenue, but the data infrastructure behind the product was held together with duct tape. The same logical pipelines existed in multiple places across GUI-based tools like Alteryx, Talend, and Tableau Prep, with no single source of truth and no scalable way to make changes. My job was to consolidate everything into code without breaking anything for live clients.

The catch: I had almost no SQL experience and zero exposure to dbt, the framework we'd chosen for the transformation layer. So before I could rebuild anything, I had to teach myself—learning SQL and dbt in real time while simultaneously keeping the existing pipelines running for clients who couldn't afford a single day of broken data.

That meant every day was a balancing act: maintaining and debugging the legacy GUI workflows to keep reports flowing on time, while carving out space to design the system that would replace them.

## Owning the Full ELT Stack

As I dug into the problem, I realized that rebuilding the transformation layer alone wouldn't be enough. The fragmentation ran through every stage of the pipeline, and to actually fix this, I'd need to own the full ELT stack.

**Extract:** Extraction was handled by an offshore team pulling data from manual portals. I trained them on standardized workflows using bash scripts to invoke pipelines consistently.

**Load:** I built a Python-based ingestion engine driven by JSON spec files, where each pipeline had its own configuration that defined how files were validated, parsed, and loaded.

**Transform:** I designed a multi-tenant dbt architecture that served all clients from a single codebase, and wrote custom dbt macros encoding the business analytical logic specific to our CPG clients—sales velocity metrics, time period aggregation calculations, and inventory management metrics that had previously lived as scattered, manual calculations across the GUI tools.

## Scaling Without Additional Engineering Hires

I built the platform to handle per-tenant customizations, so each client could tailor their data models to their specific needs without forking the shared codebase. A key part of this architecture was designing the customization layer to be accessible to non-engineers. I trained the nontechnical team in basic SQL so they could create and update atomic merchant customizations themselves, removing me as a bottleneck and scaling the team's capacity without additional engineering hires.

I paired this with a custom orchestration layer on Google Cloud and managed the data warehouse migration from Snowflake to BigQuery as part of the broader overhaul.

## Results

We eliminated reliance on Alteryx, Talend, and Tableau Prep, and reduced pipeline changes from hours of manual cross-tool work to a single code commit.

Once the core infrastructure was stable, I helped the CEO evaluate and select a CTO, then partnered with him to build the application layer that surfaced this data through an embedded BI tool for clients.

## Acquisition

In March 2024, [Daasity Inc. acquired Red Fox Analytics](https://www.daasity.com/post/daasity-acquires-red-fox-analytics), specifically to integrate the retail CPG data infrastructure and analytical logic I'd helped build into their broader platform.
