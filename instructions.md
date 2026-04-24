

# Steps to execute

1. Read enc-product-summary.md
2. Read device-summary.md
3. Select module candidates for the application
4. For the selected candidates, review in detail (user schematics, known issues and changes)
   - Identify the right device family
   - For SoC devices, consider what CPU system fits the application
   - Identify critical features and choose the best fitting product
5. Actively look out for potential issues
6. For all main features described (explicitly including all interfaces), check how they would be realized.
   - Is the interface on the processing system side?
   - Is there a IP available from the device vendor (if so, is it free/bundled with the tool or a separate paid license)?
   - Is there 3rd party IP available? (this option only is required if there is no IP from the device vendor)
   - Document all relevant options and suggest the one you see as best fit
   - For IP questions, you have to search online.
7. Find relevant supporting materials online
   - Application notes, white papers, etc. (exclude materials from other device vendors than the one selected)
   - Papers, blog-posts, etc. (one specific blog to check: micro zed chronicals from adam taylor)
8. Document all candidates with the "why it fits" and "why it could not fit"
9. Document all critical points that must be checked in detail to prove the outcome
10. Create an executive summary (200 words or less)

# Rules

* For information about FPGA device resources, always refer to the vendor materials (folder vendor)
* Always point out why you choose a certain FPGA/SoC device family and why not the other ones (the device-family selection is a critical constraint to the SOM selection)

# Report Order

The report shall be ordered as follows

1. Executive summary
2. Device selection
3. SoM selection 
4. Analysis of critical features
5. Relevant supporting materials


