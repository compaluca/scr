# Dataset 2019 
This little repository only serves to share the dataset D-II we used in Section 4 of our paper _A preliminary study on the adoption and effectiveness of SameSite cookies as a CSRF defence_ to appear into the SecWeb 2021 workshop of the IEEE Euro S&P conference.

This dataset D-II elaborates from a set of HTTP requests flagging those that are related to state-changing actions and thus required to be protected against cross-site request forgery (CSRF). 

## Dataset overview

The excel file comprises three sheets.  

### Sheet - stats

It summarizes the data figures presented in Section 4, also considering numbers extracted from D-I, the dataset used for Mitch. The complete Mitch dataset D-I is made available by their authors [here]( https://github.com/alviser/mitch). 

### Sheet - post-auth

It presents data for the HTTP requests collected while executing the for in our 39 __post-authentication scenarios__ over 23 websites. For each request we indicate the website, whether the request was indeed associated to a state-changing action (`ground of truth`), the HTTP method of the request, whether the request was same-site or not (`MAIN_DOMAIN`), and many other computed labels that we used for our own ML-based classifier. 

### Sheet - pre-auth aggregated

It aggregates data for the HTTP requests collected while executing the for in our 24 __pre-authentication login scenarios__ over 24 websites. For each scenario we indicate the website, whether the login operation was form-based or sso-based (`category`), the number of candidate state-changing HTTP requests, their associated ground of truth, and the set of labels computed on them. 

## Dataset history and context

In 2019 we performed additional tests for CSRF while developing and training our own ML-based classifier for state-changing actions to compare and extend the work done by the authors of~\cite{DBLP:conf/eurosp/CalzavaraCFRT19}. Here, we also take pre-authentication scenarios into account. More specifically, we created 63 selenium tests for 47 websites---which consist of major e-commerce sites and sites belonging to common categories, such as entertainment software, news, etc---so to analyse the HTTP traffic of entire scenarios such as the creation of a new invoice, the addition of a new administrator, etc. These tests targeted 24 pre-authentication scenarios for 24 websites and 39 post-authentication scenarios for 23 websites. For each test we manually analysed the HTTP requests to identify the state-changing ones.

We have not published this ML related work and likely we will not do it. Indeed after the recent enforcement measures for SameSite cookies from major browsers (`LaxByDefault` in short [1]), we decided to look deeper into the impact of SameSite cookies as a CSRF defence. This is the main contribution of our SecWeb 2021 paper. The evaluation indicates that when browsers opt for `LaxByDefault` SameSite cookies defence can be very effective, namely in preventing CSRF against same-site state-changing actions that take place after authentication, and not triggered via the `GET` method. However, there are still certain CSRF variants that are not covered by SameSite cookies, and that should not be neglected. In particular, cross-site state-changing scenarios and client-side CSRF attack need to be addressed on their own, as SameSite cookies cannot prevent them. 

[1] `LaxByDefault`: as of February 2020, Chrome 80 started to enforce SSC by setting any empty SameSite cookie attribute to lax by default. We will refer to this as the `LaxByDefault` policy.
