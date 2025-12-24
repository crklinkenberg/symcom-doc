---
{"dg-publish":true,"permalink":"/topics/comparison-status-in-different-modes/"}
---


Comparison status for a source is shown in the materia-medica page. The “comparison_save_status” field, in the “pre_comparison_master_data” sql table is given different value for controlling the status of the comparison.  “comparison_save_status” values:

“0” => Blue, when editor is working on a comparison.

“1” => Yellow, when editor saves a comparison.

“2” => Green, when comparison is finally saved by the supervisor.

“3” => Orange, when supervisor is working on a comparison.