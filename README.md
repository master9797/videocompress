# videocompress

You must start compression in another thread. Ideally AsyncTask(). view the code below:

VideoCompress library for Android is open source project. I made some changes in MediaController class from "Telegram" application. Removed some unused codes and change the video size to max size 480. You can change that value in MediaController.java by changing all values which 480.

Videos which compressing with this library are stremable mp4, mdat atom is not splitted by default.

AsyncTask example:

    public class VideoCompressTask extends AsyncTask<String, String, String> {
    private compressCompleteListener compressCompleteListener;

    @Override
    protected String doInBackground(String... strings) {
        boolean isComplete = MediaController.getInstance().convertVideo(strings[0], strings[1]);

        return strings[1];
    }

    @Override
    protected void onPostExecute(String s) {
        super.onPostExecute(s);
        compressCompleteListener.onComplete(s);


    }

    public void addOnCompressComleteListener(compressCompleteListener compressCompleteListener) {
        this.compressCompleteListener = compressCompleteListener;
    }
    
compressCompleteListener class(interface):

    public interface compressCompleteListener {

     void onComplete(String path);
}

Using in program example:

    VideoCompressTask task = new VideoCompressTask();
                    task.addOnCompressComleteListener(new compressCompleteListener() {
                        @Override
                        public void onComplete(String path) {
                            // that path is compressed video path
                        }
                    });
                    task.execute(sourcePath, destPath);
    

