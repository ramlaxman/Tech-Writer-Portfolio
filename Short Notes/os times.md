According to the TADM315 document of SAP:

"CPU time and processing time are related. Processing time is an important part of the response time, but not individually measurable. While processing ABAP coding, CPU time is needed. Whether the application server can allocate CPU time for the specific task depends on the overall load on the machine. In short, processing time does not automatically mean CPU time allocation! If CPU time is in short supply, processing and response time still grow, but no real work is done! Ideally, processing and CPU time are about the same size."

"Wait time, roll-in time, load and generation time, enqueue time, database request, and (optionally) roll-wait time contribute to the dialog response time. Thus, processing time is calculated by subtracting these components from the dialog response time."
