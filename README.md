# Simple Chat

This is an simple chat app to demonstrate the realtime capability of Supabase. 

## Table schema

```sql
-- Create messages table
create table if not exists public.messages (
    id uuid not null primary key default uuid_generate_v4(),
    content text not null,
    created_at timestamp with time zone default timezone('utc' :: text, now()) not null
);

-- Set row level security
alter table public.messages enable row level security;
create policy "Anyone can view all messages" on public.messages for select using (true);
create policy "Anyone can insert a message" on public.messages for insert with check (true);

-- Enable relatime
alter publication supabase_realtime add table public.messages;
```