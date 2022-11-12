<script src="vendor/jquery/jquery-3.2.1.min.js"></script>

<link rel="stylesheet" href="vendor/jquery/jquery-ui/jquery-ui.css">
<script src="vendor/jquery/jquery-ui/jquery-ui.js" type="text/javascript"></script>

<script>
    $(document).ready(function () {
        var dropIndex;
        $("#image-list").sortable({
            	update: function(event, ui) { 
            		dropIndex = ui.item.index();
            }
        });

        $('#submit').click(function (e) {
            var imageIdsArray = [];
            $('#image-list li').each(function (index) {
                if(index <= dropIndex) {
                    var id = $(this).attr('id');
                    var split_id = id.split("_");
                    imageIdsArray.push(split_id[1]);
                }
            });

            $.ajax({
                url: 'reorderUpdate.php',
                type: 'post',
                data: {imageIds: imageIdsArray},
                success: function (response) {
                   $("#txtresponse").css('display', 'inline-block'); 
                   $("#txtresponse").text(response);
                }
            });
            e.preventDefault();
        });
    });

</script>
