<template>
    <div>
        <Navbar />
        <div class="container"><br>
            <h1>My Profile</h1><br>
            <table class="table table-striped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Id</th>
                        <th>Username</th>
                        <th>Email</th>
                    </tr>
                </thead>
                    <tbody>
                        <td>{{$auth.user.id}}</td>
                        <td>{{$auth.user.name}}</td>
                        <td>{{$auth.user.email}}</td>
                    </tbody>
            </table>
        </div>
    </div>
</template>