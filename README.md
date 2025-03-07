# concurrent_futures
This blog provides details about increasing speed of any operations using concurrent library in Python

While I was working on a project of document classification and identification of products in document using Large language models, I had to classify 85,000 documents.

I had a task to upload 85,000 documents to Azure Blob Storage which is a data storage service provided by Azure. The document upload in Azure blob storage took long time that would 
increase our delivery time. The code that I was using for upload to AzureBlobStorage was:

-->Add code


What happens here is all the documents that has to be uploaded gets loaded first in memory and then it is tranferred to Azure one by one. So after a document is fully uploaded,
the next document begins to upload and so on. So it is essentially like a series where one's end leads to the other's beginning. As you can infer, the time for uploading even 1000-
2000 documents would take 2-3 hours. Moreover, if it is 85,000 documents, it would be more than 100 hours to upload which means around 13 working days. This would consume lot of time
and is definitely not the best practice. 

What if we upload the documents in parallel? This means one document upload is independent of the other upload. One's end does not determine other's beginning. For example, if we have 
to upload 10 documents then 1st,5th,7th documents can be uploaded in parallel. The question now is how do we perform parallel uploads to Azure. How do we implement the above code and
do parallel uploads for all files?

There is a way in Python to do the same. Infact, there is an underlying principle within our computer system that does parallel computations in this case, uploads. The concept is
of workers or cores in the computer's cpu. If we can employ more workers lets say 5 workers to do our task, and each worker works on their own independent of the other workers. Then this 
will lead to faster uploads and hence reduced time. So what we would do is engage more workers to do our uploads. 

The way in Python is to use Concurrent library. As the name suggests, it deals with concurrency and performing multiple tasks at hand.
The module of futures under concurrent library assigns tasks to workers. How this is done can be understood by the following steps:

1. Define the operation you would want to run. It can be any function such as square of a number, reading of files as pdf, uploading files as in my case.
2. Assign number of workers you want to use for running the operation. For this, we use ThreadPoolExecutor which takes parameter of number of workers. (We will discuss certain key terms
   later that would provide more clarity to the overview.)
3. Submit  

