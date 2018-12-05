# videocompress

You must start compression in another thread. Ideally AsyncTask(). view the code below:

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
    

