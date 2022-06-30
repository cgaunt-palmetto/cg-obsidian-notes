## fact
  - fact_solar_project_milestones => base_milestones + [...]

## intermediate > salesforce
  - base_salesforce_opportunity_milestones => salesforce__opportunity_milestone_events + salesforce__opportunity_milestone_aggregates + [...]
  - base_alchemy_milestones => [...]
  - base_milestones => base_salesforce_opportunity_milestones + base_alchemy_milestones

## trunks > salesforce > opportunity_milestones
  - salesforce__opportunity_milestone_history => get_flow_status_event_dates
  - salesforce__opportunity_milestone_events => pivot_job_max_event_dates + pivot_job_created_dates
  - salesforce__opportunity_milestone_aggregates => pivot_job_event_counts