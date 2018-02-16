#  count post views without plugin step by step
Hi, today i will show how to show post view count without using plugin. it’s very easy, just copy below php code and past in your themes functions.php page.

```
function getPostViews($postID){
$count_key = 'post_views_count';
$count = get_post_meta($postID, $count_key, true);
if($count==''){
delete_post_meta($postID, $count_key);
add_post_meta($postID, $count_key, '0');
return "0 View";
}
return $count.' Views';
}
function setPostViews($postID) {
$count_key = 'post_views_count';
$count = get_post_meta($postID, $count_key, true);
if($count==''){
$count = 0;
delete_post_meta($postID, $count_key);
add_post_meta($postID, $count_key, '0');
}else{
$count++;
update_post_meta($postID, $count_key, $count);
}
}
// Remove issues with prefetching adding extra views
remove_action( 'wp_head', 'adjacent_posts_rel_link_wp_head', 10, 0);
```
Now you can use below in single.php page where are location do you want to show post views count? must be input in your while loop.
```
setPostViews(get_the_ID());
```
Now you can input below code where are locations in do you want to show post views count. example: index page, post excerpt, etc….
```
echo getPostViews(get_the_ID());
```
Then you can see it’s working, if you need any help or if you have any problem then you can comment below this post, then i will reply for help you. thanks all, have a nice day.

Here is article http://www.wp-tutorials.com/how-to-count-post-views-without-plugin/
