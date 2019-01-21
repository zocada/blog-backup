---
ID: 884
post_title: >
  Uploading videos to Vimeo using tus js
  client in Angular
author: Chaman
post_excerpt: ""
layout: post
permalink: >
  https://zocada.com/upload-video-vimeo-tus-js-client-angular/
published: true
post_date: 2019-01-06 10:33:35
---
<p style="text-align: center;"><a href="https://vimeo.com/">Vimeo</a> is a popular video sharing website in which users can upload, share , view and stream videos. If you are planning a project which contains sharing and streaming videos then Vimeo can take care of that for you. Vimeo provides API endpoints for all the tasks so that you can implement it in any platform using any language. We'll be implementing video upload feature in an <a href="https://angular.io/">Angular</a> application with <a href="https://github.com/tus/tus-js-client">tus js client</a>.</p>
<p>&nbsp;</p>
<h2>Step 1: Setting up Vimeo account for upload access</h2>
<p>Create a Vimeo account and verify your email address, go to <a href="https://developer.vimeo.com/apps">https://developer.vimeo.com/apps</a> to register your application by providing necessary details. Now you need to request for video upload access in your <code>app settings &gt; Permissions</code> and wait for approval. After you get permission for upload you can generate your access token in <code>Authentication &gt; Generate Access Token</code>. Give <strong>"Edit"</strong> and <strong>"Upload"</strong> scopes to your token and click <strong>"Generate"</strong>. <img class="size-medium wp-image-693 aligncenter" src="https://zocada.com/wp-content/uploads/2018/12/Screenshot-22-300x141.png" alt="token scopes" width="300" height="141" /> <img class="size-medium wp-image-694 aligncenter" src="https://zocada.com/wp-content/uploads/2018/12/Screenshot-23-300x80.png" alt="ACCESS TOKEN" width="300" height="80" /> Copy or save your access token. You will be using this access token for authenticating while making API calls. Test your access token by making a <code>HTTP GET</code> request to <code>"https://api.vimeo.com/me"</code> with <code>Authorization&gt;Bearer Token</code> and paste your access token in <a href="https://www.getpostman.com/">postman</a>. <img class="alignnone size-large wp-image-698" src="https://zocada.com/wp-content/uploads/2018/12/Screenshot-24-1024x327.png" alt="API REQUEST" width="770" height="246" /> You should get a JSON response with user details for a successful API call. The API docs is available here <a href="https://developer.vimeo.com/api/playground">Vimeo API playground</a>.  </p>
<h2>Step 2: Creating the uploader</h2>
<p>There are 3 steps to upload your video successfully to Vimeo.</p>
<ol>
<li><strong>Create the video</strong></li>
<li><strong>Upload the video file</strong></li>
<li><strong>Verify the upload</strong></li>
</ol>
<h3>Create the video</h3>
<p><strong>Prerequisites</strong>: Knowledge about <a href="https://rxjs-dev.firebaseapp.com/api">RxJS concepts</a> like observables, map, pipe, expand, EMPTY. </p>
<p>In this step you are required to make an authenticated HTTP POST request to <a href="https://api.vimeo.com/me/videos">https://api.vimeo.com/me/videos</a> with the video details like file size and upload approach in the request body so that a video will be created in Vimeo with the given details. Video name and other attributes can also be sent in this request but the above 2 attributes are mandatory.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="json">{
  "name": "{filename}",
  "upload": {
    "approach": "tus",
    "size": "{size}"
  }
}</pre>
<p>The POST request should contain the following headers.</p>
<table>
<tbody>
<tr>
<td>Authorization</td>
<td><code>bearer {access_token}</code></td>
</tr>
<tr>
<td>Content-Type</td>
<td><code>application/json</code></td>
</tr>
<tr>
<td>Accept</td>
<td><code>application/vnd.vimeo.*+json;version=3.4</code></td>
</tr>
</tbody>
</table>
<p>I'll be creating a service "upload" for this and inject this service in the required component. <code>ng g service upload</code></p>
<p>Now in your upload service import the following</p>
<pre class="EnlighterJSRAW" data-enlighter-language="null">//Used for asynchronous http request handling
import { Observable } from 'rxjs';

//Required to set custom headers and make http requests
import { HttpHeaders, HttpClient } from '@angular/common/http';</pre>
<p>Pass HttpClient as constructor parameter.</p>
<p><code class="EnlighterJSRAW" data-enlighter-language="js"> constructor(private http: HttpClient) { }</code></p>
<p>Set your access token and Vimeo API endpoint.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="js">private api = 'https://api.vimeo.com/me/videos';

//It's advised not to hardcode the API token, instead fetch it from the server after authentication.
private accessToken = 'youraccesstoken';</pre>
<p>Now we'll write the <strong>createVideo</strong> function which is responsible for creating a video in your Vimeo account. The function takes a single video file of type File as a parameter and returns an observable i.e. the HPPT POST request.</p>
<h3>Current progress:</h3>
<div>
<pre class="EnlighterJSRAW" data-enlighter-language="js">//Filename: upload.service.ts<br />
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { HttpHeaders, HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class UploadService {
  constructor(private http: HttpClient) { }
  private api = 'https://api.vimeo.com/me/videos';
  private accessToken = 'youraccesstoken';

  createVideo(file: File): Observable&lt;any&gt; {
    const body = {
      name: file.name,
      upload: {
        approach: 'tus',
        size: file.size
      }
    };
    console.log(file);
    const header: HttpHeaders = new HttpHeaders()
      .set('Authorization', 'bearer ' + this.accessToken)
      .set('Content-Type', 'application/json')
      .set('Accept', 'application/vnd.vimeo.*+json;version=3.4');
    return this.http.post(this.api, body, {
      headers: header,
      observe: 'response'
    });
  }
}
</pre>
Now go to the component where you are implementing the upload feature. I'll be implementing it in <code>upload.component.ts</code>.
<ul>
<li>Create a file input that accepts videos only.</li>
<li>Add an upload button to start the process.</li>
<li>Inject your upload service into the component.</li>
</ul>
I'll be creating a class <code>uploadFiles</code> for storing the video name, web address for uploading the video &amp; URI of the uploaded video on Vimeo.
<pre class="EnlighterJSRAW" data-enlighter-language="js">// Filename: upload.compopnent.ts
export class uploadFiles {
  constructor(public video: File, public path: string, public uploadURI: string) {
    this.video = video;
    this.path = path;
    this.uploadURI = uploadURI;
  }
}</pre>
Create a function <code>getLink</code> which takes video file, current video index, video array as parameters. This function will pass the video to the <code>createVideo</code> function in the upload service. Here you can see that the index is incremented so that the process can be repeated on the entire array.</div>
<div>For every response received, you need to create a new <code>uploafFiles</code> object and save the upload link and video link from the successful response body. I've created a <code>pendingFiles</code> array to store all the video's response details for uploading later.</div>
<div> </div>
<div>
<pre class="EnlighterJSRAW" data-enlighter-language="js">// Filename: upload.component.ts
  getLink = (video: File, index, arr) =&gt; {
    console.log('index: ' + index);
    return this.upload.createVideo(video).pipe(
      map(response =&gt; {
        const videoFile = new uploadFiles(video, response.body.link, response.body.upload.upload_link);
        this.pendingFiles.push(videoFile);
        console.log('response: ' + response);
        return {
          data: response,
          index: index + 1,
          arr: arr
        };
      })
    );
  }</pre>
Create a <code>start</code> function to run when "Upload" button is clicked. The above <code>getLink</code> function has to be called for all the videos in the array, so we use the rxjs <code>expand</code> operator to return the next video for upload until the last video in the array.</div>
<div> </div>
<div>
<pre class="EnlighterJSRAW" data-enlighter-language="js">// Filename: upload.component.ts
  public start(files: FileList) {
    this.videoList = files;
    console.log(this.videoList);

    const recursion = this.getLink(this.videoList[0], 0, this.videoList).pipe(expand(res =&gt; {
      return res.index &gt; res.arr.length - 1 ?
      EMPTY : this.getLink(this.videoList[res.index], res.index, this.videoList);
    }));

      recursion.subscribe(x =&gt; {
        if (x.index &gt; x.arr.length - 1) {
          console.log('Links generated, Starting upload');
         // All links have been generated now you can start the upload process here
        }
      });
  }</pre>
Now you can test the upload link generation feature. Once the video is created and the link is generated, you can go to your Vimeo account and see the new videos created. The response will contain <code>upload.upload_link</code> which is the URL for uploading that video. </div>
<div> </div>
<div>
<h3>Current progress:</h3>
<p>[mks_tabs nav="horizontal"]<br />[mks_tab_item title="upload.component.ts"]</p>
<pre class="EnlighterJSRAW" data-enlighter-language="js">import { Component, OnInit } from '@angular/core';
import { UploadService } from '../upload.service';
import { map, expand } from 'rxjs/operators';
import { EMPTY } from 'rxjs';

export class uploadFiles {
  constructor(public video: File, public path: string, public uploadURI: string) {
    this.video = video;
    this.path = path;
    this.uploadURI = uploadURI;
  }
}

@Component({
  selector: 'app-upload',
  template: `&lt;div style="text-align:center"&gt;
  &lt;input type="file" #file name="video" id="video" accept="video/*" multiple&gt;
  &lt;input type="button" value="Upload" (click)="start(file.files);"&gt; &lt;/div&gt;`,
  styleUrls: ['./upload.component.css']
})

export class UploadComponent implements OnInit {
  title = 'vimeo-uploader';
  videoList: FileList;
  videoLinks = [];
  pendingFiles: uploadFiles[] = [];
  constructor(private upload: UploadService) { }

  ngOnInit() {}

  public start(files: FileList) {
    this.videoList = files;
    console.log(this.videoList);
    const recursion = this.getLink(this.videoList[0], 0, this.videoList).pipe(expand(res =&gt; {
      return res.index &gt; res.arr.length - 1 ?
      EMPTY : this.getLink(this.videoList[res.index], res.index, this.videoList);
    }));

      recursion.subscribe(x =&gt; {
        if (x.index &gt; x.arr.length - 1) {
          console.log('Link generated, Starting upload');
         // All links have been generated now you can start the upload
        }
      });
  }

  getLink = (video: File, index, arr) =&gt; {
    console.log('index: ' + index);
    return this.upload.createVideo(video).pipe(
      map(response =&gt; {
        const videoFile = new uploadFiles(video, response.body.link, response.body.upload.upload_link);
        this.pendingFiles.push(videoFile);
        console.log('response: ' + response);
        return {
          data: response,
          index: index + 1,
          arr: arr
        };
      })
    );
  }
}</pre>
<p>[/mks_tab_item]<br />[mks_tab_item title="upload.service.ts"]</p>
<pre class="EnlighterJSRAW" data-enlighter-language="js">import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { HttpHeaders, HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class UploadService {
  constructor(private http: HttpClient) { }
  private api = 'https://api.vimeo.com/me/videos';
  private accessToken = 'yourapitoken';

  createVideo(file: File): Observable&lt;any&gt; {
    const body = {
      name: file.name,
      upload: {
        approach: 'tus',
        size: file.size
      }
    };
    console.log(file);
    const header: HttpHeaders = new HttpHeaders()
      .set('Authorization', 'bearer ' + this.accessToken)
      .set('Content-Type', 'application/json')
      .set('Accept', 'application/vnd.vimeo.*+json;version=3.4');
    return this.http.post(this.api, body, {
      headers: header,
      observe: 'response'
    });
  }
}</pre>
<p>[/mks_tab_item]<br />[/mks_tabs]</p>
<h3> </h3>
<h3>Upload the video</h3>
We'll be using <a href="https://github.com/tus/tus-js-client">tus-js-client</a> library for uploading the videos. Install the library &amp; its type definitions and import the library.
<pre class="EnlighterJSRAW" data-enlighter-language="shell">npm install --save tus-js-client
npm install --save-dev @types/tus-js-client</pre>
<code class="EnlighterJSRAW" data-enlighter-language="js">import * as tus from 'tus-js-client';</code></div>
<div>Since we are using tus-js-client it will handle the process of uploading, we just have to specify the URL for uploading that we get in the previous successful response and set the retry delays according to your requirements and thats it.</div>
<div>Create a new <code>tus.Upload</code> object with necessary parameters inside a function in upload service so that it can be called from component.</div>
<div> </div>
<div>
<pre class="EnlighterJSRAW" data-enlighter-language="null">// Filename: upload.service.ts
  public tusUpload(
    file: uploadFiles,
    i: number,
    videoArray: uploadFiles[],
    uploadArray: tus.Upload[],
    success: any,
  ): tus.Upload {
    const upload = new tus.Upload(file.video, {
      uploadUrl: file.uploadURI,
      endpoint: file.uploadURI,
      retryDelays: [0, 1000, 3000, 5000],
      onError: error =&gt; {
        console.log('Failed: ' + file.video.name + error);
      },
      onProgress: (bytesUploaded, bytesTotal) =&gt; {
        const percentage = ((bytesUploaded / bytesTotal) * 100).toFixed(2);
        console.log(
          'file: ' + i + ' of ' + (videoArray.length - 1) + ':',
          bytesUploaded,
          bytesTotal,
          percentage + '%'
        );
      },
      onSuccess: () =&gt; {
        console.log('Download' + file.video.name + 'from' + upload.url);
        if (i &lt; videoArray.length - 1) {
          uploadArray[i + 1].start();
        } else {
          success();
          console.log('Videos uploaded successfully');
        }
      }
    });
    return upload;
  }</pre>
 </div>
<div>Create one more function in the upload component or you can directly call the <code>tusUpload</code> function after successfully creating the links.</div>
<div> </div>
<div>
<pre class="EnlighterJSRAW" data-enlighter-language="js">// Filename: upload.component.ts
  videoUpload() {
    const success = () =&gt; {
      console.log('after video upload section');
    };
    const upload: Array&lt;any&gt; = [];
    for (let i = 0; i &lt; this.pendingFiles.length; i++) {
      upload.push(
        this.upload.tusUpload(
          this.pendingFiles[i],
          i,
          this.pendingFiles,
          upload,
          success
        )
      );
    }
    console.log('start video upload sequentially');
    upload[0].start();
  }</pre>
Note: Don't forget to call <code>videoUpload</code> function after generating links, otherwise the video wont start uploading.</div>
<div> 
<h3>Current progress:</h3>
<script src="https://gist.github.com/chaman-k/14423cd9f32fc06e5916a461757f3567.js"></script></div>
<div><strong>Note</strong>: This is one way to implement, if you want less memory usage then you can skip the unnecessary array implementations.</div>
<div>If one video fails then next video can start to upload by using similar implementation of <code>onSuccess</code> method of <code>tus.Upload</code> in <code>onError</code> method. DevTools console and network tab will come handy during debugging.😉</div>
<!-- wp:paragraph -->
<p>&nbsp;</p>
<!-- /wp:paragraph -->