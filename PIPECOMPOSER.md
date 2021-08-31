# pipecomposer
Writing declarative pipelines in Jenkins

- Write the pipeline code logic on a piece of paper or whatever suits you

- Pick a small scope as a starters. Extend later when done.

- Put comments // after each stage or section with something like //end of bla so when reworking you won’t get lost when deciding to move code around.
If happy you may decide later to remove or keep them - your or your peers pick

- Use libraries where available for repetitive work. if not - try writing your own.


- if possible, test each step or stage that involves shell shebang and quotes in advance on the command line prior to introducing it into Jenkins to avoid disappointment.
Be consistent with the shell used for tests and the one mentioned in the pipeline

- Use syntax validators - see https://www.jenkins.io/doc/book/pipeline/development/ for options.
Not 100% warranty, but it covers 90% and saves you 60% of headaches

- To speed check you need to pseudocode your pipeline and test the logic.
- Invaluable when you’re not the best programmer or want to verify complex statements and don’t want to spend days waiting for the pipeline

- Once you verified your logic, test your real code pipeline. You might end up rewriting it.

- Validate syntax and test pipeline after adding each stage

- mailext must either be configured from the admin menu of Jenkins (for which not always right are present) or use multiple ‘to:’ if needed. Sample below

to: "mail1, mail2,mail3, cc: mail4, bcc: mail5"
- Using fileExists or similar operators with expanded variables may require double quotes.
See https://support.cloudbees.com/hc/en-us/articles/360027607532-Pipeline-with-conditional-stages-based-on-a-file-existing-on-the-filesystem for details. My example below:

    APPL_NAME = "APPr"
    VIEWSRV = "3030"
    HPATH = "/foo/dataX/bla/${VIEWSRV}/${APPL_NAME}"
    DPATH = "${HPATH}"
    CSONAR_VIEW_LOCATION = fileExists "${HPATH}"
